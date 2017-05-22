<template>
    <div>
        <ul v-if="paginationNumbers" class="uk-pagination uk-margin-small-top uk-margin-small-bottom" :class="flexPosition">
            <li :class="{ 'uk-disabled': pagination.current_page == 1 }">
                <a href="" @click.prevent="changePage(pagination.current_page - 1)">
                    <span uk-pagination-previous></span>
                </a>
            </li>
            <li v-if="from > 1">
                <a href="" @click.prevent="changePage(1)">1</a>
            </li>
            <li class="uk-disable" v-if="from > 1">
                <span>...</span>
            </li>
            <li v-for="page in paginationNumbers" :class="{ 'uk-active': page == pagination.current_page }">
                <a href="" @click.prevent="changePage(page)">{{ page }}</a>
            </li>
            <li class="uk-disable" v-if="to < pagination.last_page">
                <span>...</span>
            </li>
            <li v-if="to < pagination.last_page">
                <a href="" @click.prevent="changePage(pagination.last_page)">{{ pagination.last_page }}</a>
            </li>
            <li :class="{ 'uk-disabled': pagination.last_page == pagination.current_page }">
                <a href="" @click.prevent="changePage(pagination.current_page + 1)">
                    <span uk-pagination-next></span>
                </a>
            </li>
        </ul>
        <small v-if="info" class="uk-flex" :class="flexPosition ">
            Page {{ pagination.current_page }} of {{ pagination.last_page }}
        </small>
    </div>
</template>

<script>
export default {
    name: 'PaginationKit',

    props: {
        pagination: {
            type: Object,
            required: true
        },
        pageShow: {
            type: Number,
            default: 7
        },
        info: {
            type: Boolean,
            default: true
        },
        position: {
            type: String,
            default: 'center'
        }
    },

    data () {
        return {
            from: 1,
            to: 1
        }
    },

    computed: {
        paginationNumbers () {
            if (!this.pagination.to) {
                return []
            }

            if (this.pageShow % 2 == 0) console.warn('The number of `pageShow` is even, try the odd number.')

            // if (this.pageShow > this.pagination.last_page) console.error('Your `pagination.last_page` less than `pageShow`')

            if (this.pagination.current_page > Math.ceil(this.pageShow / 2)) {
                this.from = this.pagination.current_page - Math.floor(this.pageShow / 2);
            }
            
            if (this.pagination.last_page - this.pagination.current_page < Math.floor(this.pageShow / 2)) {
                this.from = this.pagination.last_page - (this.pageShow - 1);
            }

            this.to = this.from + (this.pageShow - 1);
            
            if (this.to >= this.pagination.last_page) {
                this.to = this.pagination.last_page
            }

            let numbers = []

            for (let page = this.from; page <= this.to; page++) {
                if (page > 0) numbers.push(page)
            }

            return numbers
        },

        flexPosition () {
            let position = 'uk-flex-center'

            if (this.position == 'left') position = 'uk-flex-left'
            if (this.position == 'right') position = 'uk-flex-right'

            return position
        }
    },

    methods: {
        changePage (page) {
            document.activeElement.blur()

            this.pagination.current_page = page
            
            this.$emit('change-page', page)
        }
    }
}
</script>