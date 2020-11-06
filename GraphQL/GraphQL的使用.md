#### 下载依赖

```bash
npm install -S apollo-cache-inmemory apollo-client apollo-link apollo-link-context apollo-link-http
```

#### 配置

1. 先引入依赖包

   ```js
   import {ApolloClient} from 'apollo-client'
   import {HttpLink} from 'apollo-link-http'
   import {InMemoryCache} from 'apollo-cache-inmemory'
   import VueApollo from 'vue-apollo'
   import {ApolloLink} from 'apollo-link'
   ```

2. 配置请求路径

   ```js
   const apiLink = new HttpLink({
     uri: 'http://127.0.0.1:8080/v2/api' , //请求路径
     
     uri: `${API_CONFIG.baseURL}/graphql`  //请求路径（第二种方式）
   })
   ```

3. 中间件添加请求头（如果不需要略掉这一步）

   ```javascript
   const middlewareLink = new ApolloLink((operation, forward) => {
     const token = sessionStorage.getItem('access_token')
     operation.setContext({
       headers: {
         Authorization: `Bearer ${token}` || null
       }
     })
     return forward(operation)
   })
   ```

4. 创建Apollo连接

   ```js
   const apiClient = new ApolloClient({
     link: middlewareLink.concat(apiLink),   //如果不添加请求头直接放路径
     cache: new InMemoryCache()
   })
   ```

5. 如果需要使用两个路径，例如一个添加请求头，一个不需要加

   ```js
   const apolloProvider = new VueApollo({
     clients: {
       api: apiClient,   //需要添加请求头
       base: baseClient   //不需要添加请求头
     },
     defaultClient: baseClient   //默认请求路径、如果只有一个请求头就使用这个就行
   })
   ```

6. 在vue中引入

   ```js
   Vue.use(VueApollo)
   new Vue({
     el: '#app',
     router,
     provide: apolloProvider.provide()  //需要添加这个
   })
   ```

   