# vue-slide

# Demo

The demo page is [HERE](http://hilongjw.github.io/vue-slide/demo.html).

# Instllation

## npm

```shell
$ npm install vue-slide
```

# Usage

app.vue

```html
<template>
    <div class="container">
        <!-- pagination example -->
        <div class="timeline">
            <div 
                class="item"
                @click='turnTo (1)'
                :class='{"active": slide.init.currentPage == 1}'
            >page1</div>
            <div 
                class="item"
                @click='turnTo (2)'
                :class='{"active": slide.init.currentPage == 2}'
            >page2</div>
            <div 
                class="item"
                @click='turnTo (3)'
                :class='{"active": slide.init.currentPage == 3}'
            >page3</div>
        </div>

        <!-- next and pre method -->
        <img 
            src="./assets/images/slide-arrow.svg" 
            class="slider-left"
            @click='slidePre'
            :class='{"disable": !this.slide.init.canPre}'
        >
        <img 
            src="./assets/images/slide-arrow.svg" 
            class="slider-right"
            @click='slideNext'
            :class='{"disable": !this.slide.init.canNext}'
        >

        <!-- bind inti and pageList -->

        <slide :pages="pages" :slide="slide">
        
            <!-- slot  -->
            <div class="slider-item page1" :style="pages[0].style">
                <h1>page1</h1>
                <button @click="turnTo(2)">to page2</button>
            </div>
            <div class="slider-item page2" :style="pages[1].style">
                <h1>page2</h1>
                <button @click="turnTo(3)">to page3</button>
            </div>
            <div class="slider-item page3" :style="pages[2].style">
                <h1>page3</h1>
                <button @click="turnTo(1)">to page1</button>
            </div>

        </slide>
    </div>
    
</template>
<script>
import slide from 'vue-slide'
export default {
    data () {
        return {
            slide: {
                init: {
                    pageNum: 3,
                    currentPage: 1,
                    canPre : false,
                    canNext: true,
                    start: {},
                    end: {},
                    tracking: false,
                    thresholdTime: 500,
                    thresholdDistance: 100
                }
            }
            
        }
    },
    computed: {
        pages () {
            let pageList = []

            for (let i = 0; i < this.slide.init.pageNum; i++) {
                pageList.push({
                        origin: i * 100,
                        current: 0,
                        style:{
                            'transform': `translateX(${ i*100 }%)`
                        }
                    })
            }

            return pageList
        }
    },
    methods: {
        turnTo (num) {
            this.$broadcast('slideTo', num)
        },
        slideNext () {
            this.$broadcast('slideNext')
        },
        slidePre () {
            this.$broadcast('slidePre')
        }
    },
    components: {
        slide
    }
}
</script>


```


# License

[The MIT License](http://opensource.org/licenses/MIT)

