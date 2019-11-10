<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      The universe is full of the unknown.
      You can discover a part of it searching photos captured by NASA.
    </p>
    <p class="subclaim">
      Type anything space-related to start your journey.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claimWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: white;
  }
  .claim {
    font-size: 50px;
    margin: 0;
    @media (min-width: 768px) {
      font-size: 80px;
    }
  }
  .subclaim {
    margin: 20px 0 0 0;
    font-size: 15px ;
    max-width: 500px;
    @media (min-width: 768px) {
      font-size: 20px;
      letter-spacing: 1px;
      line-height: 1.2;
    }
  }
</style>
