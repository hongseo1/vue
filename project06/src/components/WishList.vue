<!--WishList.vue-->
<template lang="html">
    <section>
        <ul>
            <li v-for="wishItem in wishItems" class="shadow">
                <i class="checkBtn fas fa-check" aria-hidden="turn"></i>
                {{wishItem}}
                <span class="removeBtn" type="button" @click="removeWish">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </ul>
    </section>
</template>
<script>
    export default{
        data(){
            return{
                wishItems: []
            }
        },
        methods:{
            removeWish(){
                console.log('clicked');
            }
        },
        created(){
            if(localStorage.length>0){
                for(var i=0; i<localStorage.length; i++){
                    this.wishItems.push(localStorage.key(i));
                }
            }
        }
    }
</script>
<style lang="css" scoped>
    ul{list-style-type: none; padding-left: 0; margin-top: 0; text-align: left;}
    li{display: flex; min-height: 50px; height: 50px; line-height: 50px; margin: 0.5em 0; padding: 0 0.9em; background: #fefefe; border-radius: 5px; overflow: hidden; text-overflow: ellipsis;}
    .checkBtn{line-height: 50px; color: #ff8000; margin-right: 5px;}
    .removeBtn{margin-left: auto; color: #de4343;}
</style>
