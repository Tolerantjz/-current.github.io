<template>
    <div id="app">
    	<div class="box">
        <div v-for="(v,index) in list">
        	<div>
            	<p :class = "{light:isLight}" @click="handleClick(null,index)"><span :class = '{triangle:isTriangle}'ref = "down"></span>{{v.title}}</p>
            </div>
            <transition-group name = 'fade'>
				<p v-show='isShowList[index]' ref = "slideFade" key = "test">{{v.context}}</p>
            </transition-group>
        </div>
      </div> 
    </div>
</template>

<script>
    const list=[
        {
            title:'What is a dog?',
            context:'A dog is a type of domesticated animal. Known for its loyalty and faithfulness, it can be found as a welcome guest in many households across the world.'
        },
        {
            title:'What kinds of dogs are there?',
            context:'There are many breeds of dogs. Each breed varies in size and temperament. Owners often select a breed of dog that they find to be compatible with their own lifestyle and desires from a companion.'
        },
        {
            title:'How do you acquire a dog?',
            context:'Three common ways for a prospective owner to acquire a dog is from pet shops, private owners, or shelters. A pet shop may be the most convenient way to buy a dog. Buying a dog from a private owner allows you to assess the pedigree and upbringing of your dog before choosing to take it home. Lastly, finding your dog from a shelter, helps give a good home to a dog who may not find one so readily.'
        }
    ]
    export default {
        data () {
            return {
                list,
                isShowList:[false,false,false],
                isLight:true,
                isTriangle:true
            }
        },
        methods:{
		    handleClick(e,index){
		      const list=[false,false,false]
		      if(this.isShowList[index] === false){
			    	this.$refs.down[index].classList.add('down')	
		      }else{
			    	this.$refs.down[index].classList.remove('down')	
		      }
		      this.isShowList[index]=!this.isShowList[index]
		      list[index]=this.isShowList[index]
		      this.isShowList=Object.assign([],list)
		    }
		  }
    }
</script>

<!--<style src = "./animate.min.css"></style>-->
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
  background-color: black;
  border-radius: 10px;
}
.light:hover{color:lightgray;cursor: pointer;}
.triangle{width: 0;height: 0;border-top:5px solid transparent;border-right:5px solid transparent;border-left: 5px solid white;border-bottom: 5px solid transparent;display: inline-block;transition: all .5s;}
.triangle.down{border-top:5px solid white;border-right:5px solid transparent;border-left: 5px solid transparent;border-bottom: 5px solid transparent;margin-top:5px ;display: inline-block;}
.box{padding: 10px;}
/*.fade-enter-active,.fade-leave-active{
	transition: all .5s;
}

.fade-enter,.fade-leave-active{
	opacity: 0;
	transform: scaleY(0);
}*/
.fade-enter-active{
	animation:fade-in .5s;
}
.fade-leave-active{
	animation:fade-out .5s;
}
@keyframes fade-in{
	from{transform: scaleY(0);opacity: 0;}
	to{transform: scaleY(1);opacity: 1;}
}
@keyframes fade-out{
	from{transform: scaleY(1);opacity: 1;}
	to{transform: scaleY(0);opacity: 0;}
}

</style>
