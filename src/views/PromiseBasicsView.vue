<script setup>
  let promise = new Promise((resolve, reject) => {
    // the function is executed automatically when the promise is constructed

    // reject(new Error('error message'))

    // after 1 second signal that the job is done with the result "done"
    setTimeout(() => resolve("done"), 1000);
  })

  promise.then(
    result => console.log(result),
    error => console.error(error)
  )

  // Delay with a promise
  function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }

  delay(3000).then(() => console.log('runs after 3 sec'))
</script>

<template>
  <h2>Promise Basics</h2>

</template>