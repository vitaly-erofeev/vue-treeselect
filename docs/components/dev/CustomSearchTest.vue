<template>
  <div>
    showSearchTip: {{ showSearchTip }}<br>
    search: {{ search }}<br>
    searchLoading: {{ searchLoading }}<br>
    searchLoaded: {{ searchLoaded }}
    <treeselect
      ref="treeselect"
      :options="options"
      :disable-immediate-search="true"
      :async="true"
      :cache-options="false"
      :append-to-body="true"
      :load-options="loadOptions"
      @search-change="onSearchChange"
      >
      <template slot="before-list">
        <div v-show="showSearchTip" class="vue-treeselect__tip vue-treeselect__seacrh-promt-tip">
          <div class="vue-treeselect__icon-container">
            <span class="vue-treeselect__icon-warning" />
          </div>
          <span class="vue-treeselect__tip-text vue-treeselect__seacrh-promt-tip-text">
            Press enter to search
          </span>
        </div>
      </template>
    </treeselect>
  </div>
</template>

<script>
  import { ASYNC_SEARCH } from '@riophae/vue-treeselect'

  export default {
    data() {
      return {
        search: null,
        searchLoading: false,
        searchLoaded: false,
        options: [
          { id: 1, label: 'bus' },
          { id: 2, label: 'table' },
          { id: 3, label: 'chair' },
          { id: 4, label: 'key' },
          { id: 5, label: 'immediate' },
          { id: 6, label: 'button' },
          { id: 7, label: 'apple' },
          { id: 8, label: 'toast' },
          { id: 9, label: 'computer' },
          { id: 10, label: 'company' },
          { id: 11, label: 'water' },
        ],
      }
    },
    computed: {
      showSearchTip() {
        return this.search && !this.searchLoading && !this.searchLoaded
      },
    },
    methods: {
      onSearchChange(value) {
        this.search = value
        this.searchLoaded = false
      },
      loadOptions({ action, callback }) {
        if (action === ASYNC_SEARCH) {
          this.searchLoaded = false
          this.searchLoading = true
          setTimeout(() => {
            this.searchLoading = false
            this.searchLoaded = true
            callback(null, this.options)
          }, 1000)
        }
      },
    },
  }
</script>

<style scoped>
</style>
