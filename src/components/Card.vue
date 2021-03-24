<template>
<div class="card">
   <img
      :src="movie.Poster"
      :alt="movie.Title"
    />

  <h3> {{movie.Title}} </h3>
</div>
</template>

<script>
export default {
  props: ['movie']
}
</script>



<style lang="scss" scoped>
.card{
  padding: 0px 8px;
  margin-bottom: 16px;
  border-radius: 2px;
  display: inline-block;
  margin: 1rem;
  position: relative;
  width: 300px;

  img{
    width: 100%;
    height: 250px;
    object-fit: cover;
    border-radius: 8px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.20);
    transition: 0.4s;
  }
  h3{
    padding: 16px;
    color: 	#f0e9e9;

  }

  &:hover {
    img{
      transform: scale(1.02);
    }

    h3 {
      color: 	#1e9427;
    }

  }
}

</style>
