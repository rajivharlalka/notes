# If need to work with async request on a array of elemets, a async for loop works better than foreach or map.

```js
for async(const element of elemenet){
    //doSomething
}
```