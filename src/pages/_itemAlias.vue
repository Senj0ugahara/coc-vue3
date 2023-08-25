<template>
  <div class="wrapper-person">
    <div v-if="item">
      <img :src="item.img" :alt="item.descr">
      <h1 class="title" style="color: #fff">{{ item.title }}</h1>
      <p>{{ item.descr }}</p>

      <div class="card-stats">
        <div
          class="one-third"
          v-for="(stat, index) in item.info"
          :key="index"
        >
          <div class="stat-value">{{stat.value}}</div>
          <div class="stat">{{stat.title}}</div>
        </div>
      </div>

      <br />
      <div>
        <router-link to="/" class="btn btnPrimary">Back to home</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import items from '@/seeders/items.js';

export default {
  data () {
    return {
      item: null
    }
  },
  created () {
    const alias = this.$route.params.itemAlias;
    const item = items.find(el => el.alias === alias);

    if (item === undefined) {
      return this.$router.push('/404');
    }

    this.item = item;
  }
}
</script>

<style lang="scss" scoped>
.wrapper-person {
  text-align: center;
}
.card-stats {
  margin: 30px 0;
  border-radius: 14px;
}
</style>