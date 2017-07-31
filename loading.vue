<template>
    <div class="loading">

        <h2>倒计时</h2>
        <p v-text="nowTime"></p>
    </div>

</template>
<script>
    export default{
        data(){
            return{
                endTime: '2017/7/31 16:00:00',
                nowTime: ''
            }
        },
        methods:{
            downTime(endTime,startTime){    // 结束时间和开始时间
                var startTime = startTime || new Date().getTime();   //获取当前时间的毫秒值
                var endTime =  (new Date(endTime)).getTime();   //获取结束时间的毫秒值

                var time = Math.floor((endTime - startTime)/1000)

                let timerId = setInterval(()=>{
                    time--;
                    // 把时间转换成天-时-分-秒
                    var d = Math.floor(time/(24*3600))
                    var h = Math.floor( time/3600%12);
                    var m = Math.floor( time/60%60);
                    var s = Math.floor( time%60);

                    d = ("0"+d).slice(-2)
                    h = ("0"+h).slice(-2)
                    m = ("0"+m).slice(-2)
                    s = ("0"+s).slice(-2)
                    if(time == 0){
                        clearInterval(timerId)
                    }

                    if(d == '00'){
                        this.nowTime = h+":"+m+":"+s
                    }else{
                        this.nowTime = d+"-"+h+":"+m+":"+s
                    }
                    console.log(this.nowTime)
                },1000)
                
            },

        },
        mounted(){
            this.downTime(this.endTime)
        },
        components:{
        }
    }
</script>