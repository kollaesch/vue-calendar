
<style scoped>
.calendar {
    margin:auto;
    width: 100%;
    min-width:300px;
    background: #fff;
    font-family: "PingFang SC","Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;
    user-select:none;
}

.calendar-tools{
    height:40px;
    font-size: 20px;
    line-height: 40px;
    color:#5e7a88;
}
.calendar-tools span{
    cursor: pointer;
}
.calendar-prev{
    width: 14.28571429%;
    float:left;
    text-align: center;
}
.calendar-info{
    padding-top: 3px;
    font-size:16px;
    line-height: 1.3;
    text-align: center;
}
.calendar-info>div.month{
    margin:auto;
    height:20px;
    width:100px;
    text-align: center;
    color:#5e7a88;
    overflow: hidden;
    position: relative;
}
.calendar-info>div.month .month-inner{
    position: absolute;
    left:0;
    top:0;
    height:240px;
    transition:top .5s cubic-bezier(0.075, 0.82, 0.165, 1);
}
.calendar-info>div.month .month-inner>span{
    display: block;
    font-size: 14px;
    height:20px;
    width:100px;
    overflow: hidden;
    text-align: center;
}
.calendar-info>div.year{
   font-size:10px;
   line-height: 1;
   color:#999;
}
.calendar-next{
    width: 14.28571429%;
    float:right;
    text-align: center;
}
 
.calendar table {
    clear: both;
    width: 100%;
    margin-bottom:10px;
    border-collapse: collapse;
    color: #444444;
}
.calendar td {
    margin:2px !important;
    padding:0px 0;
    width: 14.28571429%;
    height:44px;
    text-align: center;
    vertical-align: middle;
    font-size:14px;
    line-height: 125%;
    cursor: pointer;
    position: relative;
    vertical-align: top;
}
.calendar td.week{
    font-size:10px;
    pointer-events:none !important;
    cursor: default !important;    
}
.calendar td.disabled {
    color: #ccc;
    pointer-events:none !important;
    cursor: default !important;
}
.calendar td.disabled div{
    color: #ccc;
}
.calendar td span{
    display:block;
    max-width:40px;
    height:26px;
    font-size: 16px;
    line-height:26px;
    margin:0px auto;
    border-radius:20px;
}
.calendar td:not(.selected) span:not(.red):hover{
    background:#f3f8fa;
    color:#444;
}
.calendar td:not(.selected) span.red:hover{
    background:#f9efef;
}

.calendar td:not(.disabled) span.red{
    color:#ea6151;
}
.calendar td.selected span{
    background-color: #5e7a88;
    color: #fff;
}
.calendar td .text{
    position: absolute;
    top:28px;
    left:0;
    right:0;
    text-align: center;
    
    padding:2px;
    font-size:8px;
    line-height: 1.2;
    color:#444;
}
.calendar td .isGregorianFestival,
.calendar td .isLunarFestival{
    color:#ea6151;
}
.calendar td.selected span.red{
    background-color: #ea6151;
    color: #fff;
}
.calendar td.selected span.red:hover{
    background-color: #ea6151;
    color: #fff;
}
.calendar thead td {
  text-transform: uppercase;
  height:30px;
  vertical-align: middle;
}
.calendar-button{
    text-align: center;
}
.calendar-button span{
    cursor: pointer;
    display: inline-block;
    min-height: 1em;
    min-width: 5em;
    vertical-align: baseline;
    background:#5e7a88;
    color:#fff;
    margin: 0 .25em 0 0;
    padding: .6em 2em;
    font-size: 1em;
    line-height: 1em;
    text-align: center;
    border-radius: .3em;
}
.calendar-button span.cancel{
    background:#efefef;
    color:#666;
}
.calendar-years{
    position: absolute;
    left:0px;
    top:60px;
    right:0px;
    bottom:0px;
    background:#fff;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap:wrap;
    overflow: auto;
    transition:all .5s cubic-bezier(0.075, 0.82, 0.165, 1);
    opacity: 0;
    pointer-events: none;
    transform: translateY(-10px);
}
.calendar-years.show{
    opacity: 1;
    pointer-events: auto;
    transform: translateY(0px);
}
.calendar-years>span{
    margin:1px 5px;
    display: inline-block;
    width:60px;
    line-height: 30px;
    border-radius: 20px;
    text-align:center;
    border:1px solid #fbfbfb;
    color:#999;
}
.calendar-years>span.active{
    border:1px solid #5e7a88;
    background-color: #5e7a88;
    color:#fff; 
}
</style>

<template>
    <div class="calendar">
        <div class="calendar-tools">
            <span class="calendar-prev" @click="prev">
                <svg width="20" height="20" viewBox="0 0 16 16" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <g class="transform-group">
                    <g transform="scale(0.015625, 0.015625)">
                        <path d="M671.968 912c-12.288 0-24.576-4.672-33.952-14.048L286.048 545.984c-18.752-18.72-18.752-49.12 0-67.872l351.968-352c18.752-18.752 49.12-18.752 67.872 0 18.752 18.72 18.752 49.12 0 67.872l-318.016 318.048 318.016 318.016c18.752 18.752 18.752 49.12 0 67.872C696.544 907.328 684.256 912 671.968 912z" fill="#5e7a88"></path>
                    </g>
                </g>
                </svg>
            </span>
            <span class="calendar-next"  @click="next">
                <svg width="20" height="20" viewBox="0 0 16 16" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <g class="transform-group">
                    <g transform="scale(0.015625, 0.015625)">
                        <path d="M761.056 532.128c0.512-0.992 1.344-1.824 1.792-2.848 8.8-18.304 5.92-40.704-9.664-55.424L399.936 139.744c-19.264-18.208-49.632-17.344-67.872 1.888-18.208 19.264-17.376 49.632 1.888 67.872l316.96 299.84-315.712 304.288c-19.072 18.4-19.648 48.768-1.248 67.872 9.408 9.792 21.984 14.688 34.56 14.688 12 0 24-4.48 33.312-13.44l350.048-337.376c0.672-0.672 0.928-1.6 1.6-2.304 0.512-0.48 1.056-0.832 1.568-1.344C757.76 538.88 759.2 535.392 761.056 532.128z" fill="#5e7a88"></path>
                    </g>
                </g>
                </svg>
            </span>
            <div class="calendar-info" @click.stop="changeYear">
                <!-- {{monthString}} -->
                <div class="month">
                    <div class="month-inner" :style="{'top':-(this.month*20)+'px'}">
                        <span v-for="m in months">{{m}}</span>
                    </div>
                </div>
                <div class="year">{{year}}</div>
            </div>
        </div>
        <table cellpadding="5">
        <thead>
            <tr>
                <td v-for="week in weeks" class="week">{{week}}</td>
            </tr>
        </thead>
        <tbody>
        <tr v-for="(day,k1) in days" style="{'animation-delay',(k1*30)+'ms'}">
            <td v-for="(child,k2) in day" :class="{'selected':child.selected,'disabled':child.disabled}" @click="select(k1,k2,$event)">
                <span :class="{'red':k2==0||k2==6||((child.isLunarFestival||child.isGregorianFestival) && lunar)}">{{child.day}}</span>
                <div class="text" v-if="child.eventName!=undefined">{{child.eventName}}</div>
                <div class="text" :class="{'isLunarFestival':child.isLunarFestival,'isGregorianFestival':child.isGregorianFestival}" v-if="lunar">{{child.lunar}}</div>
            </td>
        </tr>
        </tbody>
        </table>

        <div class="calendar-years" :class="{'show':yearsShow}">
            <span v-for="y in years" @click.stop="selectYear(y)" :class="{'active':y==year}">{{y}}</span>
        </div>
 
    </div>
</template>

<script>
import calendar from './calendar.js'
export default {
    props: {
        // Multiple selection mode
        multi: {
            type: Boolean,
            default: false
        },
        // Range mode
        range:{
            type: Boolean,
            default: false
        },
        // Default date
        value: {
            type: Array,
            default: function(){
                return []
            }
        },
        // Start selecting date
        begin:  {
            type: Array,
            default: function(){
                return []
            }
        },
        // End selection date
        end:  {
            type: Array,
            default: function(){
                return []
            }
        },

        // Is it less than 10 zero padding?
        zero:{
            type: Boolean,
            default: false
        },
        // Shielded date
        disabled:{
            type: Array,
            default: function(){
                return []
            }
        },
        // Whether to display the lunar calendar
        lunar: {
            type: Boolean,
            default: false
        },

        // weekday names
        weeks: {
            type: Array,
            default:function(){
                // return window.navigator.language.toLowerCase() == "zh-cn"?['日', '一', '二', '三', '四', '五', '六']:['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
                return window.navigator.language.toLowerCase() == "de-de"?['So', 'Mon', 'Die', 'Mi', 'Do', 'Fr', 'Sa']:['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
            }
        },
        // monthnames
        months:{
            type: Array,
            default:function(){
                // return window.navigator.language.toLowerCase() == "zh-cn"?['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月']:['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
                return window.navigator.language.toLowerCase() == "zh-cn"?['Januar', 'Februar', 'März', 'April', 'Mai', 'Juni', 'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember']:['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
            }
        },
        // Custom event
        events:  {
            type: Object,
            default: function(){
                return {}
            }
        },
    },
    data() {
        return {
            years:[],
            yearsShow:false,
            year: 0,
            month: 0,
            day: 0,
            days: [],
            multiDays:[],
            today: [],
            festival:{
                lunar:{
                    "1-1":"Chinese New Year",
                    "1-15":"Lantern Festival",
                    "2-2":"Faucet festival",
                    "5-5":"Dragon Boat Festival",
                    "7-7":"Qixi Festival",
                    "7-15":"Zhongyuan Festival",
                    "8-15":"Mid-Autumn Festival",
                    "9-9":"Double Ninth Festival",
                    "10-1":"Cold clothes festival",
                    "10-15":"Lower Yuan Festival",
                    "12-8":"Laba Festival",
                    "12-23":"Jizao Festival",
                },
                gregorian:{
                    // "1-1":"New years",
                    // "2-14":"Valentine's Day",
                    // "3-8":"Women's Day",
                    // "3-12":"Arbor Day",
                    // "4-5":"Ching Ming Festival",
                    // "5-1":"Labor day",
                    // "5-4":"Youth festival",
                    // "6-1":"Children's day",
                    // "7-1":"Party building festival",
                    // "8-1":"Army Day",
                    // "9-10":"Teachers' Day",
                    // "10-1":"National Day",
                    // "12-24":"Christmas Eve",
                    // "12-25":"Christmas",
                    // https://www.feiertage-deutschland.de/2019/
                    "1-1":"Neujahr",
                    "1-6":"Heilige Drei Könige (BW,BY,ST)",
                    "3-8":"Frauentag",
                    "4-18":"Gründonnerstag (BW)",
                    "4-19":"Karfreitag",
                    "4-22":"Ostermontag",
                    "5-1":"Tag der Arbeit",
                    "5-30":"Christi Himmelfahrt",
                    "6-10":"Pfingstmontag",
                    "6-20":"Fronleichnam (BW,BY,HE,NW,RP,SL,SN,TH)",
                    "8-15":"Mariä Himmelfahrt (BY,SL)",
                    "9-20":"Weltkindertag (TH)",
                    "10-3":"Tag der Deutschen Einheit",
                    "10-31":"Reformationstag (BB,HB,HH,MV,NI,SH,SN,ST,TH)",
                    "11-1":"Allerheiligen (BW,BY,NW,RP,SL)",
                    "11-20":"Buss- und Bettag (BY,SN)",
                    "12-25":"1. Weihnachtstag",
                    "12-26":"2. Weihnachtstag",
                },
            },
            rangeBegin:[],
            rangeEnd:[],
        }
    },
    watch:{
        events(){
            this.render(this.year,this.month)
        },
        value(){
            this.init();
        }
    },
    mounted() {
        this.init()
    },
    methods: {
        init(){
            let now = new Date();
            this.year = now.getFullYear()
            this.month = now.getMonth()
            this.day = now.getDate()
            if (this.value.length>0) {
                if (this.range) { //range
                    this.year = parseInt(this.value[0][0])
                    this.month = parseInt(this.value[0][1]) - 1
                    this.day = parseInt(this.value[0][2]) 

                    let year2 = parseInt(this.value[1][0])
                    let month2 = parseInt(this.value[1][1]) - 1
                    let day2 = parseInt(this.value[1][2]) 

                    this.rangeBegin = [this.year, this.month,this.day]
                    this.rangeEnd = [year2, month2 , day2]
                }else if(this.multi){//Multiple selection
                    this.multiDays=this.value;
                    this.year = parseInt(this.value[0][0])
                    this.month = parseInt(this.value[0][1]) - 1
                    this.day = parseInt(this.value[0][2]) 
                }else{ //Radio
                    this.year = parseInt(this.value[0])
                    this.month = parseInt(this.value[1]) - 1
                    this.day = parseInt(this.value[2]) 
                }
            }
            this.render(this.year, this.month)
        },
        // Render date
        render(y, m) {
            let firstDayOfMonth = new Date(y, m, 1).getDay()         //First day of the month
            let lastDateOfMonth = new Date(y, m + 1, 0).getDate()    //The last day of the month
            let lastDayOfLastMonth = new Date(y, m, 0).getDate()     //The last day of the last month
            this.year = y
            let seletSplit = this.value
            let i, line = 0,temp = [],nextMonthPushDays = 1
            for (i = 1; i <= lastDateOfMonth; i++) {
                let day = new Date(y, m, i).getDay() //Return the day of the week（0～6）
                let k
                // first row
                if (day == 0) {
                    temp[line] = []
                } else if (i == 1) {
                    temp[line] = []
                    k = lastDayOfLastMonth - firstDayOfMonth + 1
                    for (let j = 0; j < firstDayOfMonth; j++) {
                        // console.log("first row",lunarYear,lunarMonth,lunarValue,lunarInfo)
                        temp[line].push(Object.assign(
                            {day: k,disabled: true},
                            this.getLunarInfo(this.computedPrevYear(),this.computedPrevMonth(true),k),
                            this.getEvents(this.computedPrevYear(),this.computedPrevMonth(true),k),
                        ))
                        k++;
                    }
                }
       
                
                if (this.range) { // range
                    // console.log("Date range",this.getLunarInfo(this.year,this.month+1,i))
                    let options = Object.assign(
                        {day: i},
                        this.getLunarInfo(this.year,this.month+1,i),
                        this.getEvents(this.year,this.month+1,i),
                     )
                    if (this.rangeBegin.length > 0) {
                        let beginTime = Number(new Date(this.rangeBegin[0], this.rangeBegin[1], this.rangeBegin[2]))
                        let endTime = Number(new Date(this.rangeEnd[0], this.rangeEnd[1], this.rangeEnd[2]))
                        let stepTime = Number(new Date(this.year, this.month, i))
                        if (beginTime <= stepTime && endTime >= stepTime) {
                            options.selected = true
                        }
                    }
                    if (this.begin.length>0) {
                        let beginTime = Number(new Date(parseInt(this.begin[0]),parseInt(this.begin[1]) - 1,parseInt(this.begin[2])))
                        if (beginTime > Number(new Date(this.year, this.month, i))) options.disabled = true
                    }
                    if (this.end.length>0){
                        let endTime = Number(new Date(parseInt(this.end[0]),parseInt(this.end[1]) - 1,parseInt(this.end[2])))
                        if (endTime <  Number(new Date(this.year, this.month, i))) options.disabled = true
                    }
                    if (this.disabled.length>0){
                        if (this.disabled.filter(v => {return this.year === v[0] && this.month === v[1]-1 && i === v[2] }).length>0) {
                            options.disabled = true
                        }
                    }
                    temp[line].push(options)
                }else if(this.multi){//Multiple selection
                    let options
                    // Determine whether it is selected
                    if(this.value.filter(v => {return this.year === v[0] && this.month === v[1]-1 && i === v[2] }).length>0 ){
                        options = Object.assign({day: i,selected:true},this.getLunarInfo(this.year,this.month+1,i),this.getEvents(this.year,this.month+1,i))
                    }else{
                        options = Object.assign({day: i,selected:false},this.getLunarInfo(this.year,this.month+1,i),this.getEvents(this.year,this.month+1,i))
                        if (this.begin.length>0) {
                            let beginTime = Number(new Date(parseInt(this.begin[0]),parseInt(this.begin[1]) - 1,parseInt(this.begin[2])))
                            if (beginTime > Number(new Date(this.year, this.month, i))) options.disabled = true
                        }
                        if (this.end.length>0){
                            let endTime = Number(new Date(parseInt(this.end[0]),parseInt(this.end[1]) - 1,parseInt(this.end[2])))
                            if (endTime <  Number(new Date(this.year, this.month, i))) options.disabled = true
                        }
                        if (this.disabled.length>0){
                            if (this.disabled.filter(v => {return this.year === v[0] && this.month === v[1]-1 && i === v[2] }).length>0) {
                                options.disabled = true
                            }
                        }
                    }
                    
                    temp[line].push(options)
                } else { // Radio
                     // console.log(this.lunar(this.year,this.month,i));
                    
                    let chk = new Date()
                    let chkY = chk.getFullYear()
                    let chkM = chk.getMonth()
                    // Match the last selected date
                    if (parseInt(seletSplit[0]) == this.year && parseInt(seletSplit[1]) - 1 == this.month && parseInt(seletSplit[2]) == i) {
                        // console.log("Match the last selected date",lunarYear,lunarMonth,lunarValue,lunarInfo)
                        temp[line].push(Object.assign(
                            {day: i,selected: true},
                            this.getLunarInfo(this.year,this.month+1,i),
                            this.getEvents(this.year,this.month+1,i),
                        ))
                        this.today = [line, temp[line].length - 1]
                    }
                     // Show today date when there is no default value
                    else if (chkY == this.year && chkM == this.month && i == this.day && this.value == "") {

                        // console.log("today",lunarYear,lunarMonth,lunarValue,lunarInfo)
                        temp[line].push(Object.assign(
                            {day: i,selected: true},
                            this.getLunarInfo(this.year,this.month+1,i),
                            this.getEvents(this.year,this.month+1,i),
                        ))
                        this.today = [line, temp[line].length - 1]
                    }else{
                        // Ordinary date
                        // console.log("Set optional range",i,lunarYear,lunarMonth,lunarValue,lunarInfo)
                        let options = Object.assign(
                            {day: i,selected:false},
                            this.getLunarInfo(this.year,this.month+1,i),
                            this.getEvents(this.year,this.month+1,i),
                        )
                        if (this.begin.length>0) {
                            let beginTime = Number(new Date(parseInt(this.begin[0]),parseInt(this.begin[1]) - 1,parseInt(this.begin[2])))
                            if (beginTime > Number(new Date(this.year, this.month, i))) options.disabled = true
                        }
                        if (this.end.length>0){
                            let endTime = Number(new Date(parseInt(this.end[0]),parseInt(this.end[1]) - 1,parseInt(this.end[2])))
                            if (endTime <  Number(new Date(this.year, this.month, i))) options.disabled = true
                        }
                        if (this.disabled.length>0){
                            if (this.disabled.filter(v => {return this.year === v[0] && this.month === v[1]-1 && i === v[2] }).length>0) {
                                options.disabled = true
                            }
                        }
                        temp[line].push(options)
                    }
                }
                // Wrap to Saturday
                if (day == 6 && i < lastDateOfMonth) {
                    line++
                }else if (i == lastDateOfMonth) {
                    // line++
                    let k = 1
                    for (let d=day; d < 6; d++) {
                         // console.log(this.computedNextYear()+"-"+this.computedNextMonth(true)+"-"+k)
                        temp[line].push(Object.assign(
                            {day: k,disabled: true},
                            this.getLunarInfo(this.computedNextYear(),this.computedNextMonth(true),k),
                            this.getEvents(this.computedNextYear(),this.computedNextMonth(true),k),
                        ))
                        k++
                    }
                    // The date starting next month in addition to the date of supplement
                    nextMonthPushDays=k
                }
            } //end for

            // console.log(this.year+"/"+this.month+"/"+this.day+":"+line)
            // Supplement the sixth line to make the vision stable
            if(line<=5 && nextMonthPushDays>0){
                // console.log({nextMonthPushDays:nextMonthPushDays,line:line})
                for (let i = line+1; i<=5; i++) {
                    temp[i] = []
                    let start=nextMonthPushDays+(i-line-1)*7
                    for (let d=start; d <= start+6; d++) {
                        temp[i].push(Object.assign(
                            {day: d,disabled: true},
                            this.getLunarInfo(this.computedNextYear(),this.computedNextMonth(true),d),
                            this.getEvents(this.computedNextYear(),this.computedNextMonth(true),d),
                        ))
                    }  
                }
            }
            this.days = temp
        },
        computedPrevYear(){
            let value=this.year
            if(this.month-1<0){
                value--
            }
            return value
        },
        computedPrevMonth(isString){
            let value=this.month
            if(this.month-1<0){
                value=11
            }else{
                value--
            }
            // For display purposes (the general month starts from 0)
            if(isString){
                return value+1
            }
            return value
        },
        computedNextYear(){
            let value=this.year
            if(this.month+1>11){
                value++
            }
            return value
        },
        computedNextMonth(isString){
            let value=this.month
            if(this.month+1>11){
                value=0
            }else{
                value++
            }
            // For display purposes (the general month starts from 0)
            if(isString){
                return value+1
            }
            return value
        },
        // Get lunar information
        getLunarInfo(y,m,d){
            let lunarInfo=calendar.solar2lunar(y,m,d)
            let lunarValue=lunarInfo.IDayCn
            // console.log(lunarInfo)
            let isLunarFestival=false
            let isGregorianFestival=false
            if(this.festival.lunar[lunarInfo.lMonth+"-"+lunarInfo.lDay]!=undefined){
                lunarValue=this.festival.lunar[lunarInfo.lMonth+"-"+lunarInfo.lDay]
                isLunarFestival=true
            }else if(this.festival.gregorian[m+"-"+d]!=undefined){
                lunarValue=this.festival.gregorian[m+"-"+d]
                isGregorianFestival=true
            }
            return {
                lunar:lunarValue,
                isLunarFestival:isLunarFestival,
                isGregorianFestival:isGregorianFestival,
            }
        },
        // Get custom events
        getEvents(y,m,d){
            if(Object.keys(this.events).length==0)return false;
            let eventName=this.events[y+"-"+m+"-"+d]
            let data={}
            if(eventName!=undefined){
                data.eventName=eventName
            }
            return data
        },
        // last month
        prev(e) {
            e.stopPropagation()
            if (this.month == 0) {
                this.month = 11
                this.year = parseInt(this.year) - 1
            } else {
                this.month = parseInt(this.month) - 1
            }
            this.render(this.year, this.month)
            this.$emit('selectMonth',this.month+1,this.year)
            this.$emit('prev',this.month+1,this.year)
        },
        //  Next month
        next(e) {
            e.stopPropagation()
            if (this.month == 11) {
                this.month = 0
                this.year = parseInt(this.year) + 1
            } else {
                this.month = parseInt(this.month) + 1
            }
            this.render(this.year, this.month)
            this.$emit('selectMonth',this.month+1,this.year)
            this.$emit('next',this.month+1,this.year)
        },
        // Selected date
        select(k1, k2, e) {
            if (e != undefined) e.stopPropagation()
                // Date range
            if (this.range) {
                if (this.rangeBegin.length == 0 || this.rangeEndTemp != 0) {
                    this.rangeBegin = [this.year, this.month,this.days[k1][k2].day]
                    this.rangeBeginTemp = this.rangeBegin
                    this.rangeEnd = [this.year, this.month, this.days[k1][k2].day]
                    this.rangeEndTemp = 0
                    
                } else {
                    this.rangeEnd = [this.year, this.month,this.days[k1][k2].day]
                    this.rangeEndTemp = 1
                        // Judging that the end date is less than the start date is automatically reversed
                    if (+new Date(this.rangeEnd[0], this.rangeEnd[1], this.rangeEnd[2]) < +new Date(this.rangeBegin[0], this.rangeBegin[1], this.rangeBegin[2])) {
                        this.rangeBegin = this.rangeEnd
                        this.rangeEnd = this.rangeBeginTemp
                    }
                    // Less than 10 left patch
                    let begin=[]
                    let end=[]
                    if(this.zero){
                        this.rangeBegin.forEach((v,k)=>{
                            if(k==1)v=v+1
                            begin.push(this.zeroPad(v))
                        })
                        this.rangeEnd.forEach((v,k)=>{
                            if(k==1)v=v+1
                            end.push(this.zeroPad(v))
                        })
                    }else{
                        begin=this.rangeBegin
                        end=this.rangeEnd
                    }
                    // console.log("选中日期",begin,end)
                    this.$emit('select',begin,end)
                }
                this.render(this.year, this.month)
            }else if (this.multi) {
                // Filtered if it has been selected
                let filterDay=this.multiDays.filter(v => {
                  return this.year === v[0] && this.month === v[1]-1 && this.days[k1][k2].day === v[2]
                })
                if( filterDay.length>0 ){
                    this.multiDays=this.multiDays.filter(v=> {
                      return this.year !== v[0] || this.month !== v[1]-1 || this.days[k1][k2].day !== v[2]
                    })
                }else{
                    this.multiDays.push([this.year,this.month+1,this.days[k1][k2].day]);
                }
                this.days[k1][k2].selected = !this.days[k1][k2].selected
                this.$emit('select',this.multiDays)
            } else {
                // Cancel last selected
                if (this.today.length > 0) {
                    this.days.forEach(v=>{
                        v.forEach(vv=>{
                            vv.selected= false
                        })
                    })
                }
                // Set the currently selected day
                this.days[k1][k2].selected = true
                this.day = this.days[k1][k2].day
                this.today = [k1, k2]
                this.$emit('select',[this.year,this.zero?this.zeroPad(this.month + 1):this.month + 1,this.zero?this.zeroPad(this.days[k1][k2].day):this.days[k1][k2].day])
            }
        },
        changeYear(){
            if(this.yearsShow){
                this.yearsShow=false
                return false
            }
            this.yearsShow=true
            this.years=[];
            for(let i=~~this.year-10;i<~~this.year+10;i++){
                this.years.push(i)
            }
        },
        selectYear(value){
            this.yearsShow=false
            this.year=value
            this.render(this.year,this.month)
            this.$emit('selectYear',value)
        },
        // Return today
        setToday(){
            let now = new Date();
            this.year = now.getFullYear()
            this.month = now.getMonth()
            this.day = now.getDate()
            this.render(this.year,this.month)
            // Traversing the current day to find the selected
            this.days.forEach(v => {
                let day=v.find(vv => {
                    return vv.day==this.day && !vv.disabled
                })
                if(day!=undefined ){
                  day.selected=true  
                }
                
            })
        },
        // Date zero
        zeroPad(n){
            return String(n < 10 ? '0' + n : n)
        },
    }
}

</script>
