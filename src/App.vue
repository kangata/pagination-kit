<template>
    <div class="uk-container uk-margin-medium-top uk-margin-medium-bottom   ">
        <h4 class="uk-heading-line uk-text-center"><span>UIkit 3 default</span></h4>
        <pagination :pagination="pagination" v-on:change-page="changePage"></pagination>

        <h4 class="uk-heading-line uk-text-center"><span>UIkit 3 no info</span></h4>
        <pagination :pagination="pagination" v-on:change-page="changePage" :info="false"></pagination>

        <h4 class="uk-heading-line uk-text-center"><span>UIkit 3 custom page show</span></h4>
        <pagination :pagination="pagination" v-on:change-page="changePage" :page-show="pageShow"></pagination>

        <h4 class="uk-heading-line uk-text-center"><span>UIkit 3 position left</span></h4>
        <pagination :pagination="pagination" v-on:change-page="changePage" position="left"></pagination>

        <h4 class="uk-heading-line uk-text-center"><span>UIkit 3 position right</span></h4>
        <pagination :pagination="pagination" v-on:change-page="changePage" position="right"></pagination>
    </div>
</template>

<script>
import Pagination from './UIkit-3.vue'

export default {
    name: 'PaginationKit',

    components: {
        Pagination
    },

    data () {
        return {
            pagination: {
                current_page: 1,
                from: 1,
                last_page: 25,
                per_page: 4,
                to: 1,
                total: 100
            },
            pageShow: 5
        }
    },

    methods: {
        changePage(page) {
            console.log(page)
        }
    }
}
</script>