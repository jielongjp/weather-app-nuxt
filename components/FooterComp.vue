<template>
  <footer>
    <a href="https://github.com/jielongjp/" target="_blank">
      <img src="../assets/GitHub-Mark.png" alt="Github Logo">
    </a>
    <p>Made by Jielong</p>
  </footer>
</template>

<script>
export default {
  name: 'FooterComp'
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nanum+Brush+Script&family=Raleway:wght@100&display=swap');

footer {

    font-family: 'Nanum Brush Script';
    font-size: 1.4rem;
    overflow: hidden;
    background-color: rgb(45, 44, 44);
    width: 100%;
    margin-top: 15px;
    display:flex;
    justify-content: center;
    }

footer a {
    margin-right: 5px;
}

footer p {
    margin-top: 8px;
}

</style>
