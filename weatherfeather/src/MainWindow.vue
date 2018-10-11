<template>
  <Window title="weatherfeather" width="400" height="100" margined v-on:close="exit">
    <Box padded>
      <Text>Lets see the weather, we hope it's light as a feather!!</Text>
      <Box horizontal padded>
        <TextInput stretchy></TextInput>
        <Button stretchy>Lets have a look then, shall we??</Button>
      </Box>
    </Box>
  </Window>
</template>

<script>
export default {
  methods: {
    exit() {
      this.$exit();
    },
  },
};
</script>
