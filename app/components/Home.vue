<template>
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Wakeup man"></Label>
        </ActionBar>

        <ScrollView>
            <StackLayout class="home-panel">
                <!--Add content here-->
                <StackLayout orientation="vertical" width="100%" height="1000" id="clock">
                    <Label class="time"> {{time}} </Label>
                    <Label class="date"> {{date}} </Label>
                </StackLayout>
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    export default {

        data () {
            return {
               time: "",
               date: "",
               week: ['DOM', 'SEG', 'TER', 'QUA', 'QUI', 'SEX', 'SAB']
            };
        },
        computed: {
            message() {
                return "Blank {N}-Vue app";
            }
            
            
        },
        mounted() {
            this.updateTime();
            setInterval(this.updateTime, 1000);
        },
        methods: {
            updateTime: function() {
                let cd = new Date();
                this.time = this.zeroPadding(cd.getHours(), 2)  + ':' + this.zeroPadding(cd.getMinutes(), 2) + ':' + this.zeroPadding(cd.getSeconds(), 2);
                this.date = this.zeroPadding(cd.getFullYear(), 4) + '-' + this.zeroPadding(cd.getMonth()+1, 2) + '-' + this.zeroPadding(cd.getDate(), 2) +  this.week[cd.getDay()];;
            },
            zeroPadding: function (num, digit) {
                let zero = '';
                for(var i = 0; i < digit; i++) {
                    zero += '0';
                }
                return (zero + num).slice(-digit);
            }
        }
    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '../app-variables';
    // End custom common variables

    // Custom styles
    Page {
        background: #0f3854;
        // background: radial-gradient(ellipse at center,  #0a2e38  0%, #000000 70%);
        // background-size: 100%;
        // height: 100%;
    }
    // .fa {
    //     color: $accent-dark;
    // }


    Label {
        margin: 0;
        padding: 0;
    }

    #clock {
        font-family: 'Share Tech Mono', monospace;
        color: #ffffff;
        text-align: center;
        position: absolute;
        left: 50%;
        top: 100;
        color: #daf6ff;
        text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(10, 175, 230, 0);
    }

    .time {
        letter-spacing: 0.05em;
        font-size: 40%;
        padding: 5px 0;
    }
    .date {
        letter-spacing: 0.1em;
        font-size: 20%;
    }
</style>
