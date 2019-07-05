<template>
    <div class="feed" ref="feed">
        <ul v-if="contact">
            <li v-for="message in messages" :class="`message${message.to == contact.id ? ' sent' : ' received'}`" :key="message.id">
                <div class="text">
                    {{ message.text }}
                </div>
            </li>
        </ul>
    </div>
</template>
<script>
import { setTimeout } from 'timers';
export default {
     props: {
         contact: {
             type: Object
         },
         messages: {
             type: Array,
             required: true
         }
     },
     methods: {
         scrollToBottom(){
             setTimeout(() => {
                 this.$refs.feed.scrollTop = this.$refs.feed.scrollHeight - this.$refs.feed.clientHeight;
             }, 50)
         }
     },
     watch: {
         contact(contact){
             this.scrollToBottom();
         },
         messages(messages){
             this.scrollToBottom();
         }
     }
}
</script>
<style lang="scss" scoped>
.feed {
    height: 100%;
    background: #f0f0f0;
    max-height: 473px;
    overflow: scroll;

    ul {
        list-style: none;
        padding: 5px;

        li {

            &.message {
                margin: 10px 0;
                width: 100%;

                .text {
                    max-width: 270px;
                    border-radius: 4px;
                    padding: 12px;
                    display: inline-block;
                }

                &.received {
                    text-align: right;

                    .text {
                        background: #e0e0e0
                    }
                }

                &.sent {
                    text-align: left;

                    .text {
                        background: #63fda8
                    }
                }
            }
        }
    }
}
</style>
