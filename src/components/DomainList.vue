/* eslint-disable no-console */
<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <AppItemList
              title="Prefixos"
              v-bind:items="prefixes"
              v-on:addItem="addPrefix"
              v-on:deleteItem="deletePrefix"
            />
          </div>
          <div class="col-md">
            <AppItemList
              title="Sufixos"
              v-bind:items="sufixes"
              v-on:addItem="addSufix"
              v-on:deleteItem="deleteSufix"
            />
          </div>
        </div>
        <br />
        <h5>
          Domínios
          <span class="badge badge-info">{{ domains.length }}</span>
        </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" :key="domain.name">
                <div class="row">
                  <div class="col-md">{{ domain.name }}</div>
                  <div class="col-md text-right">
                    <a class="btn btn-info" v-bind:href="domain.checkout" target="blank">
                      <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import 'font-awesome/css/font-awesome.css';
import AppItemList from './components/AppItemList';

export default {
	name: 'app',
	components: {
		AppItemList
	},
	data: function() {
		return {
			prefixes: [],
			sufixes: []
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixes.push(prefix);
		},
		addSufix(sufix) {
			this.sufixes.push(sufix);
		},
		deletePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},
		deleteSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		}
	},
	computed: {
		domains() {
			// eslint-disable-next-line no-console
			console.log('generating domains...');
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					const name = prefix + sufix;
					const url = name.toLowerCase();
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
					domains.push({ name, checkout });
				}
			}
			return domains;
		}
	}
};
</script>

<style>
</style>
