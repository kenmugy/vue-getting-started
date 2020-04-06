<template>
  <div class="app">
    <h1>App</h1>
    <hr />
    <div class="input-field">
      <input type="text" placeholder="searching" v-model="query" />
      <button @click="handleSearch('token', $event)">click</button>
    </div>
    <div class="out">
      <output>searching for: {{ query }}</output>
    </div>
    <hr />
    <div class="input-field">
      <label
        >beers
        <input type="checkbox" value="beers" v-model="searchIndexs" />
      </label>
      <label
        >breweries
        <input type="checkbox" value="breweries" v-model="searchIndexs" />
      </label>
      <label
        >apples
        <input type="checkbox" value="apples" v-model="searchIndexs" />
      </label>
      <label
        >telephone
        <input type="checkbox" value="telephone" v-model="searchIndexs" />
      </label>
      <label
        >matooke
        <input type="checkbox" value="matooke" v-model="searchIndexs" />
      </label>
      <ul>
        <li v-for="(search, i) in searchIndexs" :key="i">
          <small>{{ search }}</small>
        </li>
      </ul>
    </div>
    <hr />
    <label>
      male
      <input type="radio" v-model="sex" value="male" />
    </label>
    <label>
      female
      <input type="radio" v-model="sex" value="female" />
    </label>
    <p>Sex selected: {{ sex }}</p>
    <hr />
    <label>location</label>
    <select v-model="location">
      <option selected disabled value>choose are of location</option>
      <option value="kampala">kampala</option>
      <option value="mukono">mukono</option>
      <option value="mbarara">mbarara</option>
      <option value="gulu">gulu</option>
      <option value="mbale">mbale</option>
    </select>
    <p>location: {{ location }}</p>
    <hr />
    <div class="btns">
      <p>event bubbling</p>
      <div @click="grand">
        <div @click="parent">
          <button @click="child">child</button>
        </div>
      </div>
      <p>event capturin</p>
      <div @click.capture="grand">
        <div @click.capture="parent">
          <button @click.capture="child">child</button>
        </div>
      </div>
      <p>other</p>
      <div @click="grand">
        <div @click.capture="parent">
          <button @click="child">child</button>
        </div>
      </div>
      <p>stop propagation</p>
      <div @click="grand">
        <div @click="parent">
          <button @click.stop="child">child</button>
        </div>
      </div>
      <p>other</p>
      <div @click="grand">
        <div @click="parent">
          <button @click="child">child</button>
        </div>
      </div>
    </div>
    <hr />
    <h5>conditional rendering</h5>
    <div>
      <div v-if="beers.length === 0">No beers were found</div>
      <div v-else-if="beers.length === 1">1 beer was found</div>
      <div v-else>{{ beers.length }} beers were found</div>
    </div>
    <hr />
    <h3>beer table</h3>
    <table>
      <tr>
        <th>Beers</th>
        <th>Prices</th>
        <th></th>
      </tr>
      <tbody>
        <tr v-for="beer in beers2" :key="beer.name">
          <td>{{ beer.name }}</td>
          <td>{{ beer.price }}</td>
          <td><button @click="buy(beer)">buy</button></td>
        </tr>
        <tr>
          <td>Total</td>
          <td>{{ subTotal }}</td>
          <td>
            <button @click="reset">
              reset
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <h5>shoppingCart</h5>
    <ul>
      <li v-for="(item, i) in shoppingCart" :key="i">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      query: '',
      searchIndexs: [],
      sex: 'male',
      location: '',
      beers: ['j', 'k', 'op'],
      beers2: [
        {
          name: 'prisner lager',
          price: 2500
        },
        {
          name: 'club prisner',
          price: 2600
        },
        {
          name: 'smirnoff black',
          price: 3500
        },
        {
          name: 'bell lager',
          price: 2800
        }
      ],
      shoppingCart: [],
      subTotal: 0.0
    };
  },
  methods: {
    handleSearch(t, e) {
      alert(
        `Token: ${t} \n Query: ${this.query} \n Event: ${e.target.textContent}`
      );
    },
    grand() {
      console.log('grand');
    },
    parent() {
      console.log('parent');
    },
    child() {
      console.log('child');
    },
    buy(px) {
      this.subTotal += px.price;
      this.shoppingCart = [...this.shoppingCart, px.name];
    },
    reset() {
      this.subTotal = 0;
      this.shoppingCart = [];
    }
  }
};
</script>

<style>
table,
td,
th {
  border: 1px solid;
  border-collapse: collapse;
  padding: 10px;
}
</style>
