<template>
  <div class="claim-wrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy,
      and discover places you never even heard of.
    </p>
    <p class="subclaim">
      Type anything space-related to start
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};

</script>

<style lang="scss" scoped>

.subclaim {
  font-size: 18px;
  font-weight: 300;
}

.claim {
  font-size: 80px;
  font-weight: bold;
}

.claim-wrapper {
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  align-items: center;
}

</style>
