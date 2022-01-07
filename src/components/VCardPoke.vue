<template>
  <article class="flex justify-between w-full bg-white rounded-2xl p-6">
    <div class="leading-9 pt-2">
      <div class="flex">
        <h4 class="font-bold">Nom :</h4>
        <p class="pl-3">{{ name }}</p>
      </div>

      <div class="flex">
        <h4 class="font-bold">:</h4>
        <p class="pl-3">{{ height }}</p>
      </div>

      <div class="flex">
        <h4 class="font-bold">Taille :</h4>
        <p class="pl-3">{{ weight }}</p>
      </div>
    </div>

    <div class="w-32">
      <img class="rounded-full" :src="image" alt="Salamèche" />
    </div>
  </article>
</template>

<script>
export default {
  name: 'VCardPoke',

  props: {
    name: {
      type: String,
      required: true,
    },

    height: {
      type: String,
      required: true,
    },

    weight: {
      type: String,
      required: true,
    },

    image: {
      type: String,
      required: true,
    },
  },
}
</script>

<style scoped></style>
