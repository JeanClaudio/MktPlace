<template>

<div>
    <div id="containerBanner" class="container d-flex justify-content-center">
        <img id="Imgbanner" class="" src="http://dev.owinteractive.com/produtos/1.jpg" alt="">
        <img id="Imgbanner2" class="" src="http://dev.owinteractive.com/produtos/2.jpg" alt="">
    </div>
    
    <div class="container d-flex justify-content-center">
        <button id="btn-1" @click="banner(1)"></button>
        <button id="btn-2" @click="banner(2)"></button>
    </div>
</div>

</template>

<script>
export default{
    name:'BannerHome',
    
    methods:{
        banner(val){
                let img1 = document.getElementById('Imgbanner')
                let img2 = document.getElementById('Imgbanner2')
            if(val == 1){          
                img1.style.display = 'block'
                img2.style.display = 'none'
                document.getElementById('btn-1').style.backgroundColor = '#8E37BB'
                document.getElementById('btn-2').style.backgroundColor = '#ffffff'
            }
            else if(val == 2){
                img2.style.display = 'block'
                img1.style.display = 'none'
                document.getElementById('btn-2').style.backgroundColor = '#8E37BB'
                document.getElementById('btn-1').style.backgroundColor = '#ffffff'
            }
        }
    }
}
</script>
  
<style src="./style.scss" lang="scss" scoped />