<template>
  <section class="hero">
    <div class="hero-overlay">
      <div class="middle-section">
        <h1>MOVIE LIBRARY</h1>
        <p>
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style scoped>
.hero {
  position: relative;
  width: 100vw;
  height: 100vh;
  min-height: 100vh;
  background-image: url("@/assets/images/Header Image.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  overflow: hidden;
}

.hero-overlay {
  width: 100vw;
  min-height: 100vh;
  background: rgba(0,0,0,0.6);
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.middle-section {
  width: 100vw;
  color: #fff;
  border-top: 1px solid #444;
  padding: 60px 0 60px 0;
  box-sizing: border-box;
}

.middle-section h1 {
  font-size: 3.2rem;
  font-family: 'Montserrat', Arial, sans-serif;
  font-weight: 600;
  letter-spacing: 0.08em;
  margin: 0 0 32px 0;
  text-align: left;
  padding-left: 60px;
}

.middle-section p {
  color: #fff;
  font-size: 1.15rem;
  letter-spacing: 0.04em;
  line-height: 1.5;
  margin: 0;
  text-align: left;
  max-width: 600px;
  padding-left: 60px;
}


/* Tablet */
@media only screen and (max-width:800px) {
  .middle-section {
    padding: 20px 0px 20px 0px;
  }
  .middle-section h1,
  .middle-section p {
    padding-left: 20px;
  }
  .middle-section h1 {
    font-size: 2rem;
    margin-bottom: 32px;
  }
  .middle-section p {
    font-size: 1.15rem;
    max-width: 350px;
  }
}
</style>