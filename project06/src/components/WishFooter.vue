<!--WishFooter.vue-->
<template lang="html">
    <div class="clearAllContainer">
        <span class="clearAllBtn" @click="removeModal">Clear All</span>

        <modal v-if="removeModal" @close="removeModal=false">
            <!--모달 제목-->
            <h3 slot="header">경고</h3>
            <!--모달 내용-->
            <span slot="footer" @click="removeModal= false">
                모두 삭제하시겠습니까?
                <span @click="clearWish">예</span>
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>
<script>
    import Modal from './common/Modal.vue'

    export default{
        data(){
            return{
                removeModal: false
            }
        },
        methods: {
            clearWish(){
                this.$emit('removeAll'); //$emit 상위에 있는 거 사용
                this.removeModal = !this.removeModal;
            }
        },
        components: {
            Modal: Modal
        }
    }
</script>
<style lang="css" scoped>
    .clearAllContainer{width: 7.5em; height: 50px; line-height: 50px; background: linear-gradient(to right, #ff4c4d, #b30000); border-radius: 5px; margin: 25px auto 0;}
    .clearAllBtn{font-weight: bold; text-transform: uppercase; letter-spacing: 1px; color: white; display: block; cursor: pointer;}
</style>
