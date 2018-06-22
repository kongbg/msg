<template>
    <div>
        <div id="container"></div>

        <div>
            <iframe id="mapPage" width="400px" height="400px" frameborder=0
                src="http://apis.map.qq.com/tools/locpicker?search=1&type=1&key=OB4BZ-D4W3U-B7VVO-4PJWW-6TKDJ-WPB77&referer=myapp">
            </iframe>
        </div>
    </div>
    
    
</template>

<script>
    import { TMap } from '../../assets/js/TMap'
    export default {
        data() {
            return {
                mapKey:'2R3BZ-RIE6K-DCRJE-AOADH-PRQV7-XMBWQ'
            }
        },
        components:{
        },
        created() {
            
        },
        computed: {
            data() {
                
            }
        },
        mounted() {
            this.init()
            window.addEventListener('message', function(event) {
                // 接收位置信息，用户选择确认位置点后选点组件会触发该事件，回传用户的位置信息
                var loc = event.data;
                if (loc && loc.module == 'locationPicker') {//防止其他应用也会向该页面post信息，需判断module是否为'locationPicker'
                console.log('location', loc);
                }
            }, false);
        },
        methods: {
            
            init(){
                TMap(this.mapKey).then(qq => {
                    var map = new qq.maps.Map(document.getElementById("container"), {
                        // 地图的中心地理坐标。
                        center: new qq.maps.LatLng(39.916527, 116.397128),
                        zoom: 8
                    });

                    var geolocation = new qq.maps.Geolocation(this.mapKey, "mapqq");
                    var options = {timeout: 10000};
                    geolocation.getLocation(function(p){
                        var map = new qq.maps.Map(document.getElementById("container"), {
                            // 地图的中心地理坐标。
                            center: new qq.maps.LatLng(p.lat, p.lng),
                            zoom: 10
                        });
                    }, function(e){
                        console.log(e)
                    }, function(o){
                        console.log()
                    })
                });
            }
           
        }
    }

</script>

<style scoped>
  #container{
      width: 500px;
      height: 400px;
  }
</style>
