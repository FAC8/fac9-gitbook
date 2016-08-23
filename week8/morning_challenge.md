# Promises
## WHY
If you're using **callbacks** to execute **multiple operations in sequence** (e.g. retrieve data, do something with it, retrieve more data, do something with it, etc.), **your code might look something like this**...

```js
getDataFunction('/someUrl', function(err, response){
  console.log('we are getting this response', response)
  var usefulParam = JSON.parse(response).body.param
  console.log("we'll use parameter to make another request")
  // do something
  // do something
  // do something
  // do something
  getDataFunction(`/data/${usefulParam}`, function(err2, response2){
    console.log('we are getting this response', response2)
    var usefulParam2 = JSON.parse(response).body.param2
    getDataFunction(`/data/${usefulParam2}`, function(err3, response3){
      console.log('we are getting another response', response3)
      getDataFunction(`/data/${usefulParam3}`, function(err4, response4){
        // do something
        // do something
        // do something
        // do something
        console.log('nesting is getting quite nasty...')
      })
    })
  })
})
```

And what if you needed to perform an operation only after **all of a number of operations were completed?**


## HOW