#  Runtime API Doc generation for Go-Fiber

I personally dislike OpenAPI and Swagger because of how bloated it is for small projects. It comes with way too many features which I personally don't think I will ever use. 
Along with this, creating swagger docs in Go inside comments is nothing short of a bad Developer Experience.

So since one of my most recurring use case is be able to share some type of API docuemtnation with my UI developer, and I cannot be bothered to write and verify stuff in comments with absolutely no auto-comepletion of type check, I wanted to create a very minimal runtime-api-doc generation tool, which registers all your routes on fiber along with the Request Body Type and creates a very simple documentation meant for sharing with your other developers so they understand what you are up to.
It currently only supports GET and POST request, and comes with a bunch of "OPINIONATED" request handler wrappers, which makes my workflow 100x faster (not exggerating).

Some features include
1. Auto documentation generation - Being able to serve it on any route you need with any level of authentication.
2. Function wrappers for GET and POST requests, where handlers can just be functions / methods which take 1 argument of any DTO you have declared for that route (So your handler would look like `createStore(details StoreDetails)` instead of the pathetic `createStore(ctx *fiber.Ctx)` - Now things get more composable and you can call stuf from within one another without having to pass around a ctx you don't need.. 
3. Pre-Validating your request body before feeding it to your handler (as 1 argument).
4. Post-request error handling + Response structuring. All your handlers return (any, error) which can be used to construct predictable response structures and handle errors with appropriate http codes using the custom `RequestError` implememtion of `error`.
4. Being able to access ctx via closure and keeping handler clean and typed at all times (so they are composable) - Ex. `createStore(data StoreData, queryData QueryData)` where `queryData` can be gotten using a special `getExtras(ctx *fiber.Ctx)` method call, where you can use `ctx` for the 2 times you need it in your application. 

I have no plans to maintain this further, but I will explore porting this to non-Fiber frameworks as well, if I want to use them.
The swagger like UI can be made better as well and probably will be. 


Open Source - Take it


