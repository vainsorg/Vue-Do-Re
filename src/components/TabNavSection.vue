<template>
    <div style="margin-top: 50px;" class="container" >
        <div class="row">
            <div style="border: 1px solid white" class="col-md-9">
                <div class="row">
                    
                </div>
                <div style="background:color rgb(246, 246, 246);">

                    <b-tabs content-class="mt-3">
                        
                        <b-tab title="Öne Çıkanlar" active>
                            <div class="row">
                                <div class="col-md-4"
                                v-for="(post,index) in posts"
                                v-bind:item="post"
                                v-bind:index="index"
                                v-bind:key="post.id"
                                >
                                <b-card
                                v-bind:title=post.isim
                                v-bind:img-src=post.resim
                                img-alt="Image"
                                img-top
                                tag="article"
                                class="mb-2"
                                >
                                    <b-card-text>
                                    {{post.fiyat}} TL
                                    </b-card-text>
                                    <b-button @click="tikla(post.id)" class="buttons" href="" variant="primary">SEPETE EKLE</b-button>
                                                                
                                </b-card>
                                
                                </div>
                            </div>
                        </b-tab>
                        
                        <b-tab title="Çok Satanlar">
                            <div class="row">
                                <div class="col-md-4"
                                v-for="(urunler,index) in urun2"
                                v-bind:item="urunler"
                                v-bind:index="index"
                                v-bind:key="urunler.id"
                                >
                                <b-card
                                v-bind:title=urunler.isim
                                v-bind:img-src=urunler.resim
                                img-alt="Image"
                                img-top
                                tag="article"
                                class="mb-2"
                                >
                                    <b-card-text>
                                    {{urunler.fiyat}} TL
                                    </b-card-text>
                                    <b-button @click="tikla(urunler.id)" class="buttons" href="" variant="primary">SEPETE EKLE</b-button>
                                                                
                                </b-card>
                                
                                </div>
                            </div>
                        </b-tab>
                        <b-tab title="İndirimli Ürünler" >
                            <div class="row">
                                <div class="col-md-4"
                                v-for="(post,index) in posts"
                                v-bind:item="post"
                                v-bind:index="index"
                                v-bind:key="post.id"
                                >
                                <b-card
                                v-bind:title=post.isim
                                v-bind:img-src=post.resim
                                img-alt="Image"
                                img-top
                                tag="article"
                                class="mb-2"
                                >
                                    <b-card-text>
                                    {{post.fiyat}} TL
                                    </b-card-text>
                                    <b-button @click="tikla(post.id)" class="buttons" href="" variant="primary">SEPETE EKLE</b-button>
                                                                
                                </b-card>
                                
                                </div>
                            </div>
                        </b-tab>
                        
                        <b-tab title="Yeni Ürünler" >
                            <div class="row">
                                <div class="col-md-4"
                                v-for="(urunler,index) in urun2"
                                v-bind:item="urunler"
                                v-bind:index="index"
                                v-bind:key="urunler.id"
                                >
                                <b-card
                                v-bind:title=urunler.isim
                                v-bind:img-src=urunler.resim
                                img-alt="Image"
                                img-top
                                tag="article"
                                class="mb-2"
                                >
                                    <b-card-text>
                                    {{urunler.fiyat}} TL
                                    </b-card-text>
                                    <b-button @click="tikla(urunler.id)" class="buttons" href="" variant="primary">SEPETE EKLE</b-button>
                                                                
                                </b-card>
                                
                                </div>
                            </div>
                        </b-tab>
                    </b-tabs>
            </div>
            </div>
            <div style="border: 1px solid rgb(246,246,246)" class="col-md-3">
                <div style="height:80px;">
                        <h3 style="margin-top:10px; color:black; font-weight: bold;">Özel Ürünler</h3>
                </div>
                
                     <div class="col-md-12">
                                    <div>
                                <b-card
                                    v-bind:title=this.urun2[3].isim
                                    v-bind:img-src=this.urun2[3].resim
                                    img-alt="Image"
                                    img-top
                                    tag="article"
                                    class="mb-2"
                                >
                                    <b-card-text>
                                    {{this.urun2[3].fiyat}} TL
                                    </b-card-text>

                                    <b-button @click="tikla(9)"  class="buttons" href="#" variant="primary">SEPETE EKLE</b-button>
                                </b-card>
                                </div>
                                </div>
                                 <div class="col-md-12">
                                    <div>
                                <b-card
                                    v-bind:title=this.urun2[1].isim
                                    v-bind:img-src=this.urun2[1].resim
                                    img-alt="Image"
                                    img-top
                                    tag="article"
                                    class="mb-2"
                                    style="font-size: 12px;"
                                >
                                    <b-card-text>
                                    {{this.urun2[1].fiyat}} TL
                                    </b-card-text>

                                    <b-button @click="tikla(7)" class="buttons" href="#" variant="primary">SEPETE EKLE</b-button>
                                </b-card>
                                </div>
                                </div>

            </div>
        </div>
        
        <Header :msg = "toplamUrun"></Header>
    </div>
</template>

<script>
import { urunBus } from '../main'
import PostService from '../PostService'
import Urun2 from '../Urun2'

export default {
    data(){
        return{
            posts: [],
            urun2: [],
            error: '',
            id: 0,
            isim: '',
            resim: '',
            fiyat: 0
        }
    },
    
    async created() {
    try {
      this.posts = await PostService.getPosts();
      this.urun2 = await Urun2.getPosts();
    }
    catch (err){
      this.error = err.message;
    }
    },

     methods:{
        tikla(butonId){
            urunBus.$emit('urunEklendi', butonId)
            this.$bvModal.show('bv-modal-example') 
        }
    }
    
}
</script>

<style scoped>

a:link{
    color:white;
}


 .nav-tabs{
    height:80px !important;
}
.col-md-9{
    padding-right: 30px;
    border: 3px solid white;
    
}

.mb-2{
    border: 2px solid white;
    border-radius: 0%;
}
.mb-2:hover{
    border: 2px solid  rgb(166, 166, 166);
     border-radius: 0%;
}


.buttons{
    background-color: black;
    border: black;
    border-radius: 0%;
    font-size: 13px;
    font-weight: bold;
    color: white;
}

.buttons:hover{
    background-color: darkorange;
    border: black;
}

.card-title{
    font-size: 15px;
    font-weight: bold;
    color: black;
}

.card-text{
    font-size: 20px;
    font-weight:bolder;
    color: black;
}

.main-container{
    background-color: rgb(246, 246, 246);
}

.nav-item:hover{

  text-decoration: none;
  color: black;
}


</style>