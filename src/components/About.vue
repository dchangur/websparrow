<template>
    <section class="page-section bg-light text-dark mb-0" id="about">
            <div class="container">
                <!-- About Section Heading-->
                <h2 class="page-section-heading text-center text-uppercase text-dark">Technical skills</h2>
                <!-- Icon Divider-->
                <div class="divider-custom divider-primary">
                    <div class="divider-custom-line"></div>
                    <div class="divider-custom-icon"><i class="fas fa-laptop"></i></div>
                    <div class="divider-custom-line"></div>
                </div>
                <!-- About Section Content-->
                <div class="row">
 
                    <div class="col-md-4 d-none d-sm-block">
                        <div v-for="(skill, index) in skills" :key="index" v-on:click="showSkill(index)" class="pointer col-md-12 alert shadow-sm"  :class="{ 'btn-primary' : skill.showSkill, 'btn-outline-primary': !skill.showSkill}">
                            {{skill.skillTitle}}
                        </div>
                    </div>
                    <div class="col-md-8 d-none d-sm-block">
                        <div class="col-md-12  alert bg-white shadow-sm">
                            <div v-for="(skill, index) in skills" :key="index">
                                <div  v-if="skills[index].showSkill">
                                    <h5 class="text-left">{{skills[index].skillTitle}}</h5>
                                    <div class="progress mb-2" v-for="(skill, index) in skills[index].theSkills" :key="index">
                                        <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar" value="75" aria-valuenow="95" aria-valuemin="0" aria-valuemax="100" v-bind:style="{ width: skill.value + '%'}">{{skill.title}}</div>
                                    </div>
                                    <div v-if="skills[index].skillTitle === 'Design Skills'">
                                        <div class="row">
                                           
                                            <div class="col-lg-4" v-for="(image, index) in skills[index].theSkills" :key="index">
                                                <img :src="image.img" class="img-fluid">
                                            </div>
                                            
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>  

                <div class="row d-block d-sm-none">
                    <div class="col-md-12">
                        <div v-for="(skill, index) in skills" :key="index" class="col-md-12 alert bg-white shadow-sm">
                            <div>
                                <h5 class="text-left">{{skills[index].skillTitle}}</h5>
                                <div class="progress mb-2" v-for="(skill, index) in skills[index].theSkills" :key="index">
                                    <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar" value="75" aria-valuenow="95" aria-valuemin="0" aria-valuemax="100" v-bind:style="{ width: skill.value + '%'}">{{skill.title}}</div>
                                </div>
                            </div>                  
                        </div>
                    </div>
                </div>     
            </div>
        </section>
</template>

<script>



let skills = [{
    skillTitle: "Design Skills",
    showSkill: true,
    theSkills: [
        {title: "User experience design", value: 80, img: "../assets/img/adobe-xd.svg"},
        {title: "User interaction design", value: 80, img: "../assets/img/adobe-xd.svg"},
        {title: "Adobe XD", value: 80, img: "../assets/img/adobe-xd.svg"},
        {title: "Adobe photoshop", value: 75, img: "../assets/img/photoshop-cc.svg"},
    ]},
    {
    skillTitle: "Development Skills",
    showSkill: false,
    theSkills: [
        {title: "HTML", value: 95, img: "../assets/img/adobe-xd.svg"},
        {title: "CSS", value: 80, img: "../assets/img/adobe-xd.svg"},
        {title: "JavaScript", value: 75, img: "../assets/img/adobe-xd.svg"},
        {title: "VueJS", value: 55, img: "../assets/img/adobe-xd.svg"},
        {title: "AngularJS", value: 55, img: "../assets/img/adobe-xd.svg"},
        {title: "SASS", value: 45, img: "../assets/img/adobe-xd.svg"},
        {title: "Git", value: 65, img: "../assets/img/adobe-xd.svg"},
    ]},
    {
    skillTitle: "Database Management systems",
    showSkill: false,
    theSkills: [
        {title: "MongoDB NoSQL", value: 35, img: "../assets/img/adobe-xd.svg"},
        {title: "MySQL", value: 35, img: "../assets/img/adobe-xd.svg"}
    ]},
    {
    skillTitle: "Content Management Systems",
    showSkill: false,
    theSkills: [
        {title: "Wordpress", value: 90, img: "../assets/img/adobe-xd.svg"}
    ]},
]

export default {

    data: () => ({
        skills: skills,
        showDesignSkills: false,

    }),
    methods: {
        showSkill: function (index){
            for (let i = 0; i < this.skills.length; i++){
                this.skills[i].showSkill = false;
            }
            this.skills[index].showSkill = true;
        }
    }
    
}
</script>

<style scoped>

.pointer {
    cursor: pointer;
}

.btn-outline-primary{
    background: #ffffff;
}

</style>