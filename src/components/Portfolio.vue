<template>
    <section class="page-section portfolio" id="portfolio">
            <div class="container">
                <!-- Portfolio Section Heading-->
                <h2 class="page-section-heading text-center text-uppercase text-secondary mb-0">Portfolio</h2>
                <!-- Icon Divider-->
                <div class="divider-custom">
                    <div class="divider-custom-line"></div>
                    <div class="divider-custom-icon"><i class="fas fa-magic"></i></div>
                    <div class="divider-custom-line"></div>
                </div>
                <!-- Portfolio Grid Items-->
                <div class="row">
                    <!-- Portfolio Item-->
                    <div class="col-md-6 col-lg-4 mb-5" v-for="(obj, key) in portfolioJSON" :key="key">
                        <div class="portfolio-item mx-auto" data-toggle="modal" :data-target="'#modal' + obj.modalId" >
                            <div class="portfolio-item-caption d-flex align-items-center justify-content-center h-100 w-100">
                                <div class="portfolio-item-caption-content text-center text-white"><i class="fas fa-plus fa-3x"></i></div>
                            </div>
                            <h2>{{obj.header}}</h2>
                            <h5>{{obj.caption}}</h5>
                            <img class="img-fluid" v-bind:src="[obj.img]" alt="" />
                        </div>
                    </div>
                </div>
            </div>
            <!-- Portfolio Modal 1-->
            <div class="portfolio-modal modal fade" v-for="(obj, key) in portfolioJSON" :key="key" v-bind:id="['modal' + obj.modalId]"  tabindex="-1" role="dialog" aria-labelledby="portfolioModal1Label" aria-hidden="true">
                <div class="modal-dialog modal-xl" role="document">
                    <div class="modal-content">
                        <button class="close" type="button" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true"><i class="fas fa-times"></i></span>
                        </button>
                        <div class="modal-body text-center">
                            <div class="container">
                                <div class="row justify-content-center">
                                    <div class="col-lg-8">
                                        <!-- Portfolio Modal - Title-->
                                        <h2 class="portfolio-modal-title text-secondary text-uppercase mb-0" id="portfolioModal1Label">Log Cabin</h2>
                                        <!-- Icon Divider-->
                                        <div class="divider-custom">
                                            <div class="divider-custom-line"></div>
                                            <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                                            <div class="divider-custom-line"></div>
                                        </div>
                                        <!-- Portfolio Modal - Image-->
                                        <img class="img-fluid rounded mb-5" v-bind:src="[obj.img]" alt="" />
                                        <!-- Portfolio Modal - Text-->
                                        <p class="mb-5">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Mollitia neque assumenda ipsam nihil, molestias magnam, recusandae quos quis inventore quisquam velit asperiores, vitae? Reprehenderit soluta, eos quod consequuntur itaque. Nam.</p>
                                        <button class="btn btn-primary" data-dismiss="modal">
                                            <i class="fas fa-times fa-fw"></i>
                                            Close Window
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
</template>

<script>

var portfolioJSON = [
           {
               img: ' /assets/img/portfolio/submarine.png',
               header: 'Header 1',
               caption: 'This is the caption',
               modalId: 1
           },
           {
               img: ' /assets/img/portfolio/safe.png',
               header: 'Header 2',
               caption: 'This is the caption',
               modalId: 2
           },
           {
               img: ' /assets/img/portfolio/game.png',
               header: 'Header 3',
               caption: 'This is the caption',
               modalId: 3
           },
       ] 
export default {
    data: () => ({
       portfolioJSON: portfolioJSON
    })
}
</script>

<style scoped>

</style>