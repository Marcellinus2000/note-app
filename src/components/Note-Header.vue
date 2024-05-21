<script setup>
  
</script>

<template>
  <header>
    <div class="topbar">
      <div class="imgtext">
        <img src="../assets/notes_icon.png" alt="Notes Logo">
        <h1>Notes</h1>
      </div>

      <ul>
        <RouterLink class="gap" to="/"> Home </RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </ul>
      
    </div>
  </header>
</template>



<style lang="scss" scoped>
  header{
    background-color: #f1f1f1;
    padding: 0 1%;

    .topbar{
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 8px;
    }

    ul{
      list-style: none;

      a{
        text-decoration: none;
        color: black;
      }
    }
    .gap{
      margin-right: 2rem;
    }
    .imgtext{
      display: flex;
      align-items: center;

      img{
        max-width: 50px;
      }

      h1{
        font-size: 20px;
      }
    }
    
  }
</style>