<script>
import axios from 'axios';
import dayjs from 'dayjs';

export default {
    data() {
        return {
            feeds: []
        }
    },

    mounted() {
        this.loadFeeds();
    },

    methods: {
        async loadFeeds() {
            let response = await axios.get('/feed')
            this.feeds = response.data;
        },
        getRelativeDate(date) {
            let day = dayjs(date);
            return day.fromNow();
        }
    }
}
</script>

<template>
    <div class="feeds-page">
        <h3>Друзья</h3>

        <div class="feed-post my-3">
                <div v-for="(item, index) in feeds" class="card mb-3">
                    <div class="card-body">
                        <div class="user">
                        <img :src="'src/avatars/' + item.author.avatar">

                        <div class="username">
                            {{ item.author.firstName }} {{ item.author.lastName }}
                        </div>

                        <div class="feed-post-time ms-auto">
                            {{ getRelativeDate(item.createdAt) }}
                        </div>

                    </div>

                    <p class="card-text">
                        {{ item.content }}
                    </p>

                    </div>
                </div>
            </div>

    </div>
</template>


<style>
.feed-post-time {
    font-size: 14px;
    color: #6c757d;
}

.user {
    height: 60px;
    display: flex;
    gap: 10px;
    align-items: center;
}

.user img {
    width: 50px;
    height: 50px;
    object-fit: cover;
    object-position: center;
    border-radius: 100%;
    border: 1px solid #6c757d;
}

.user .username {
    font-weight: bold;
}
</style>