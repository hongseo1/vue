<template lang="html">
    <div id="app">
        <WishHeader></WishHeader>
        <WishInput v-on:addWish="addWish"></WishInput>
        <!--v-on:addWish에 addWish는 이벤트(하위에서 함수 호출하는 이름), = "addWish"에 addWish는 App.vue에 정의한 함수-->
        <WishList v-bind:propsData="wishItems" @removeWish="removeWish" @aditWish="editWish"></WishList>
        <WishFooter v-on:removeAllOfChild="removeAllOfParents"></WishFooter>
    </div>
</template>
<script>
    import WishHeader from './components/WishHeader.vue'
    import WishInput from './components/WishInput.vue'
    import WishList from './components/WishList.vue'
    import WishFooter from './components/WishFooter.vue'

    export default{
        data(){
            return{
                wishItems: []
            }
        },
        created(){
            if(localStorage.getItem("vue-whish"){
                this.wishItems = JSON.parse(localStorage.getItem(vue-wish))
                this.wishItems.sort(function(a,b){
                    return a.key < b.key ? -1 : a.key > b.key ? 1 : 0;
                    //배열 정리 시 사용, if문은 사용할 수 없기때문에 3항 연산자 사용

                    /* 예문
                    var arr = [{key:3}], [{key:1}], [{key:2}];
                    arr.sort(function(a,b){
                        return a.key < b.key ? -1 : a.key > b.key ? 1 : 0;
                    });
                    console.log(arr);
                    */
                    // 결과 [{key:1}], [{key:2}], [{key:1}]
                });
            }
        },
        methods:{
            addWish(key, value, date){
                this.wishItems.push({
                    key,
                    value,
                    createdDate: date,
                    modifiedDate: date
                })
                localStorage.setItem("vue-wish", JSON.stringify(this.wishItems))
                /* 예문
                    let car = {
                        no : "11가 1111",
                        name : "소나타",
                        maker : "현대",
                        cc : 2000,
                        year: 2021
                    };
                */
                /* 자바스크립트 객체를  JSON 데이터로 변환
                    var json = JSON.stringify(car);
                    console.log(json);
                */
                // 결과 {"no":"11가 1111", "name":"소나타", "maker":"현대", "cc":2000, "year":2021}
            },
            clearAll(){
                localStorage.clear();
                this.wishItems= [];
            },
            removeWish(wishItem, index){
                localStorage.removeItem(wishItem);
                this.wishItems.splice(index, 1); //index 1개 제거(잘라내기)
            }
        },
        components: {
            'WishHeader' : WishHeader,
            'WishInput' : WishInput,
            'WishList' : WishList,
            'WishFooter' : WishFooter,
        }
    }
</script>
<style lang="css">
    body{
        text-align: center;
        background-color: #f6f6f8;
    }
    input{
        border-style: groove;
        width: 200px;
    }
    button{
        border-style: groove;
    }
    .shadow{
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
        }
</style>
