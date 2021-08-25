<template>
   <div class="row">
      <div class="col  q-ma-md ">
        <div class="text-h3 text-primary">{{ title }}</div>
        <div class="text-grey-7">{{ subTitle }}</div>
      </div>
    </div>
</template>

<script>
export default {
    props: ['title','subTitle']   
}
</script>

<style>

</style>