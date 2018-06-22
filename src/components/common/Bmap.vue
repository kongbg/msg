<template>
    <div id="baiduMap"></div>
</template>
<script>
    export default {
        name:'Bmap',
        data() {
            return {
                CityInfo: {
                    longitude: 116.331398,
                    latitude: 39.897445 
                },
            }
        },
        mounted() {
            this.initBaiduMap();
        },
        methods: {
            
            
            //初始化百度地图
            initBaiduMap() {
                let that = this;
                //1.动态创建一个script标签
                let script = document.createElement("script");
                //2.script.src赋值
                script.src = "http://api.map.baidu.com/api?v=2.0&ak=Ms9KhbdjD92rULvQP6cYBiz9j4glx2tq&callback=createMap";
                //3.将script标签插入页面
                document.head.appendChild(script);
                window.createMap = () => {
                    //创建Map实例
                    var map = new BMap.Map("baiduMap");//创建Map实例
                    var point = new BMap.Point(this.CityInfo.longitude, this.CityInfo.latitude)
                    map.centerAndZoom(point, 11);// 创建点坐标,初始化地图,设置中心点坐标和地图级别
                    var marker = new BMap.Marker(point);  // 创建标注
                    map.addOverlay(marker);               // 将标注添加到地图中
                    marker.setAnimation(BMAP_ANIMATION_BOUNCE); //跳动的动画
                    debugger
                    var geolocation = new BMap.Geolocation();
                    debugger
                    geolocation.getCurrentPosition(function(r){
                        debugger
                        if(this.getStatus() == BMAP_STATUS_SUCCESS){
                            that.CityInfo.longitude=r.point.lng;
                            that.CityInfo.latitude=r.point.lat;
                            // var new_point = new BMap.Point(that.CityInfo.longitude, that.CityInfo.latitude)

                            // map.centerAndZoom(new_point, 11);// 创建点坐标,初始化地图,设置中心点坐标和地图级别
                            // var new_marker = new BMap.Marker(new_point);  // 创建标注
                            // map.addOverlay(new_marker);               // 将标注添加到地图中
                            // marker.setAnimation(BMAP_ANIMATION_BOUNCE); //跳动的动画
                        
                            
                            //map.panTo(r.point);
                            
                            
                            map.enableScrollWheelZoom(true); //开启鼠标滚轮缩放
                            // alert('您的位置：'+r.point.lng+','+r.point.lat);
                        }
                        else {
                            alert('failed'+this.getStatus());
                        }        
                    });
                    
                    
                    // map.addControl(new BMap.MapTypeControl()); //添加地图类型控件
                    // map.addControl(new BMap.ScaleControl({//添加地图类型控件
                    //     anchor: BMAP_ANCHOR_BOTTOM_LEFT
                    // }));
                    // // map.addControl(new BMap.NavigationControl({//缩放工具
                    // //     anchor: BMAP_ANCHOR_BOTTOM_RIGHT
                    // // }));
                    // map.enableScrollWheelZoom(true); //开启鼠标滚轮缩放
                    // map.enableInertialDragging(); //两秒后开启惯性拖拽
                }
            },
            //初始化百度地图
            initBaiduMap3() {
                let that = this;
                //1.动态创建一个script标签
                let script = document.createElement("script");
                //2.script.src赋值
                script.src = "http://api.map.baidu.com/api?v=2.0&ak=Ms9KhbdjD92rULvQP6cYBiz9j4glx2tq&callback=createMap";
                //3.将script标签插入页面
                document.head.appendChild(script);
                window.createMap = () => {
                    //创建Map实例
                    var map = new BMap.Map("baiduMap");//创建Map实例
                    map.centerAndZoom(new BMap.Point(this.CityInfo.longitude, this.CityInfo.latitude), 11);// 创建点坐标,初始化地图,设置中心点坐标和地图级别
                    
                    var geolocation = new BMap.Geolocation();
                    geolocation.getCurrentPosition(function(r){
                        
                        if(this.getStatus() == BMAP_STATUS_SUCCESS){
                            var myGeo = new BMap.Geocoder();
                            myGeo.getLocation(new BMap.Point(r.point.lng, r.point.lat), function(result){
                                if (result){
                                    console.log('result',result)
                                }
                            })
                                 
                            
                        }


                                 
                    });
                    
                    
                  
                }
            },
        },
    }

</script>
<style scoped>
   
    #baiduMap{
        width: 100%;
        height: 450px;
        border: 1px solid #666;
    }
    
    
</style>
