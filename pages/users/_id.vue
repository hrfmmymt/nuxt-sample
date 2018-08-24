<template>
  <section class="container">
    <h1>GitHub Users</h1>
    <img :src="`https://github.com/${user.login}.png`" :alt="`${user.name} icon image`" width="300" height="300">
    <h2>{{user.name}}</h2>
    <table>
      <tbody>
        <tr v-for="(value, key) in user" :key="key">
          <th>{{key}}</th>
          <td>{{value}}</td>
        </tr>
      </tbody>
    </table>
  </section>
</template>
 
<script>
import axios from 'axios'

export default {
  layout: 'base',

  async asyncData ({ params }) {
    const { data: user } = await axios.get(`https://api.github.com/users/${params.id}`)
    return {
      user
    }
  },

  head () {
    return {
      title: this.user.name,
      meta: [
        {
          hid: 'description',
          name: this.user.name,
          content: 'My custom description'
        }
      ]
    }
  }
}
</script>
 
<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
  padding: 2%;
}

.container img {
  margin-bottom: 2%;
}

.container table {
  border-collapse: collapse;
  margin: 0 auto;
}

.container th,
.container td {
  border: 1px solid #ccc;
  padding: 1em;
}

.container th {
  background: #efefef;
}
</style>