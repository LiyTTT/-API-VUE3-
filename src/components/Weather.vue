<template>
  <el-row class="tac">
    <!-- 左导航栏，用于显示省份列表并选择 -->
    <el-col :span="3.5">
      <el-menu
        active-text-color="#ffd04b"
        background-color="#2a5caa"
        class="el-menu-vertical-demo"
        default-active="2"
        text-color="#fff"
      >
        <!-- 省份列表，点击时调用selectProvince方法 -->
        <el-menu-item index="2" @click="selectProvince('北京市')"><span>北京市</span></el-menu-item>
        <el-menu-item index="3" @click="selectProvince('天津市')"><span>天津市</span></el-menu-item>
        <el-menu-item index="4" @click="selectProvince('河北省')"><span>河北省</span></el-menu-item>
        <el-menu-item index="5" @click="selectProvince('山西省')"><span>山西省</span></el-menu-item>
        <el-menu-item index="6" @click="selectProvince('内蒙古自治区')"><span>内蒙古自治区</span></el-menu-item>
        <el-menu-item index="7" @click="selectProvince('辽宁省')"><span>辽宁省</span></el-menu-item>
        <el-menu-item index="8" @click="selectProvince('吉林省')"><span>吉林省</span></el-menu-item>
        <el-menu-item index="9" @click="selectProvince('黑龙江省')"><span>黑龙江省</span></el-menu-item>
        <el-menu-item index="10" @click="selectProvince('上海市')"><span>上海市</span></el-menu-item>
        <el-menu-item index="11" @click="selectProvince('江苏省')"><span>江苏省</span></el-menu-item>
        <el-menu-item index="12" @click="selectProvince('浙江省')"><span>浙江省</span></el-menu-item>
        <el-menu-item index="13" @click="selectProvince('安徽省')"><span>安徽省</span></el-menu-item>
        <el-menu-item index="14" @click="selectProvince('福建省')"><span>福建省</span></el-menu-item>
        <el-menu-item index="16" @click="selectProvince('山东省')"><span>山东省</span></el-menu-item>
        <el-menu-item index="15" @click="selectProvince('江西省')"><span>江西省</span></el-menu-item>
        <el-menu-item index="17" @click="selectProvince('河南省')"><span>河南省</span></el-menu-item>
        <el-menu-item index="18" @click="selectProvince('湖北省')"><span>湖北省</span></el-menu-item>
        <el-menu-item index="19" @click="selectProvince('湖南省')"><span>湖南省</span></el-menu-item>
        <el-menu-item index="20" @click="selectProvince('广东省')"><span>广东省</span></el-menu-item>
        <el-menu-item index="21" @click="selectProvince('广西壮族自治区')"><span>广西壮族自治区</span></el-menu-item>
        <el-menu-item index="22" @click="selectProvince('海南省')"><span>海南省</span></el-menu-item>
        <el-menu-item index="23" @click="selectProvince('重庆市')"><span>重庆市</span></el-menu-item>
        <el-menu-item index="24" @click="selectProvince('四川省')"><span>四川省</span></el-menu-item>
        <el-menu-item index="25" @click="selectProvince('贵州省')"><span>贵州省</span></el-menu-item>
        <el-menu-item index="26" @click="selectProvince('云南省')"><span>云南省</span></el-menu-item>
        <el-menu-item index="27" @click="selectProvince('西藏自治区')"><span>西藏自治区</span></el-menu-item>
        <el-menu-item index="28" @click="selectProvince('陕西省')"><span>陕西省</span></el-menu-item>
        <el-menu-item index="29" @click="selectProvince('甘肃省')"><span>甘肃省</span></el-menu-item>
        <el-menu-item index="30" @click="selectProvince('青海省')"><span>青海省</span></el-menu-item>
        <el-menu-item index="31" @click="selectProvince('宁夏回族自治区')"><span>宁夏回族自治区</span></el-menu-item>
        <el-menu-item index="32" @click="selectProvince('新疆维吾尔自治区')"><span>新疆维吾尔自治区</span></el-menu-item>
        <el-menu-item index="33" @click="selectProvince('香港特别行政区')"><span>香港特别行政区</span></el-menu-item>
        <el-menu-item index="34" @click="selectProvince('澳门特别行政区')"><span>澳门特别行政区</span></el-menu-item>
        <el-menu-item index="35" @click="selectProvince('台湾省')"><span>台湾省</span></el-menu-item>
      </el-menu>
    </el-col>
    <!-- 中间主体内容区域 -->
  <el-col :span="18">
    <div class="main-content">
      <!-- 天气信息展示 -->  
      <el-row>
        <el-col
          v-for="index in cityCardPlaceholders"
          :key="index"
          :span="4.5"
        >
          <el-card class="WeatherCard" shadow="always">
            <template #header>
              <div class="card-header">
                <span class="CityText">{{ selectedCities[index] || '未选择' }}</span>
                <span>{{ weatherInfo[selectedCities[index]]?.weather || '' }}</span>
              </div>
            </template>
            <div class="weather-details" v-if="selectedCities[index]">
              <div class="temperature-humidity">
                <p>{{ weatherInfo[selectedCities[index]]?.temperature }}℃</p>
                <p>{{ weatherInfo[selectedCities[index]]?.humidity }}%</p>
              </div>
              <img :src="getWeatherIcon(weatherInfo[selectedCities[index]]?.weather)" alt="Weather Icon">
            </div>
            <div v-else>
            <!-- 当没有选择城市时显示的内容 -->
              <p>请选择一个城市</p>
            </div>
            <template #footer>
              {{ weatherInfo[selectedCities[index]]?.winddirection }}风 |  {{ weatherInfo[selectedCities[index]]?.windpower }}级
            </template>
          </el-card>
        </el-col>
      </el-row>
      <hr>
      <el-row>
        <!-- 折线图 -->
        <el-col :span="14">
          <div ref="chartContainer" class="chart-container"></div>
          <div ref="maxTempChartContainer" class="chart-container"></div>
        </el-col>
        <!-- 饼图 -->
        <el-col :span="3">
          <div class="pie-chart-container" ref="pieChartContainer"></div>
        </el-col>
      </el-row>
    </div>
  </el-col>

    <!-- 右侧边栏 -->
    <el-col :span="2">
      <div class="right-sidebar">
        <!-- 显示已选城市的标签 -->
        <el-tag
          v-for="city in selectedCities"
          :key="city"
          closable
          @close="handleClose(city)"
          class="custom-city-tag">
          {{ city }}
        </el-tag>

        <!-- 下拉选择器 -->
        <el-select v-model="cityToAdd" placeholder="选择城市" @change="replaceCity">
          <el-option
            v-for="city in cities"
            :key="city"
            :label="city"
            :value="city">
          </el-option>
        </el-select>
      </div>
    </el-col>
  </el-row>
</template>

<script lang="ts" setup>

// 引入需要的库和组件
import * as echarts from 'echarts';
import { onMounted,ref, watch} from 'vue';
import axios from 'axios';

// 数据定义
const maxCityCards = 5;
const cityCardPlaceholders = Array.from({ length: maxCityCards }, (_, index) => index);
const cities = ref([]);
const selectedCities = ref<string[]>([]); // selectedCities 是一个字符串数组
const cityToAdd = ref<string>(''); // cityToAdd 是一个字符串
const chartContainer = ref(null);
const maxTempChartContainer = ref(null);
const pieChartContainer = ref(null);
const weatherFrequency = ref({});// 天气现象统计对象
const futureWeatherInfo = ref<Record<string, Array<any>>>({});  // 确保是一个记录，其值为数组
const weatherInfo = ref<Record<string, WeatherData>>({});
const selectedProvince = ref('');

// ECharts 图表实例
let maxTempChart: echarts.ECharts | null = null;
let myChart: echarts.ECharts | null = null;
let pieChart: echarts.ECharts | null = null;

// 定义天气数据接口
interface WeatherData {
  adcode: string;
  city: string;
  humidity: string;
  province: string;
  reporttime: string;
  temperature: string;
  weather: string;
  winddirection: string;
  windpower: string;
}

interface Forecast {
  daytemp: string;
  nighttemp: string;
  dayweather: string;
}

interface CityData {
  name: string;
}

// 获取天气图标
const getWeatherIcon = (weatherCondition: string) => {
  const basePath = 'http://localhost:5173/src/components/WeatherIcon/';
  switch(weatherCondition) {
    case '晴':
      return basePath + 'sunny.png';
    case '多云':
      return basePath + 'cloudy.png';
    case '小雨':
      return basePath + '小雨.png';
    case '中雨':
      return basePath + '中雨.png';
    case '大雨':
      return basePath + '大雨.png';
    case '雷阵雨':
      return basePath + '雷阵雨.png';
    case '雷阵雨并伴有冰雹':
      return basePath + '雷阵雨伴有冰雹.png';
    case '暴雨':
      return basePath + '暴雨.png';
    case '阴':
      return basePath + '阴.png';
    case '小雪':
      return basePath + '小雪.png';
    case '中雪':
      return basePath + '中雪.png';
    case '大雪':
      return basePath + '大雪.png';
    case '雨夹雪':
      return basePath + '雨夹雪.png';

    default:
      return basePath +'unknown.png'; // 默认图标
  }
};

// 获取选中的城市当前天气
const getCityWeather = async (cityName: string) => {
  const url = `https://restapi.amap.com/v3/weather/weatherInfo?city=${encodeURIComponent(cityName)}&key=ac68016432ec9cf6c1c4252d57404879`;

  try {
    const response = await axios.get(url);
    const weatherData = response.data.lives[0];

    weatherInfo.value[cityName] = {
      adcode: weatherData.adcode,
      city: weatherData.city,
      humidity: weatherData.humidity,
      province: weatherData.province,
      reporttime: weatherData.reporttime,
      temperature: weatherData.temperature,
      weather: weatherData.weather,
      winddirection: weatherData.winddirection,
      windpower: weatherData.windpower,
    };
    console.log('天气信息：',weatherData);

  } catch (error) {
    console.error('请求天气信息出错:', error);
  }
};

// 获取选中城市未来天气
const getFutureWeather = async (cityName: string) => {
  const url = `https://restapi.amap.com/v3/weather/weatherInfo?city=${encodeURIComponent(cityName)}&key=ac68016432ec9cf6c1c4252d57404879&extensions=all`;

  try {
    const response = await axios.get(url);
    const forecastData = response.data.forecasts[0];
    const dailyForecasts = forecastData.casts;
    futureWeatherInfo.value[cityName] = dailyForecasts.map((forecast: Forecast) => {
      return {
        dayTemp: forecast.daytemp,      // 最高温度
        nightTemp: forecast.nighttemp,  // 最低温度
        dayWeather: forecast.dayweather // 天气现象
      };
    });

    console.log(`天气数据 [${cityName}]:`, futureWeatherInfo.value[cityName]);
  } catch (error) {
    console.error('请求未来天气信息出错:', error);
  }
};

// 获取省份下所有城市
const getCityList = async (provinceName: string) => {
  const url = `https://restapi.amap.com/v3/config/district?keywords=${encodeURIComponent(provinceName)}&subdistrict=1&key=ac68016432ec9cf6c1c4252d57404879`;

  try {
    const response = await axios.get(url);
    const cityData = response.data.districts[0].districts;
    cities.value = cityData.map((city: CityData) => city.name);
    
    selectedCities.value = cities.value.slice(0, Math.min(5, cities.value.length));// 更新selectedCities为该省份的前五个城市
  } catch (error) {
    console.error('请求城市列表出错:', error);
  }
};

// 处理关闭城市标签
const handleClose = (cityToRemove: string) => {
  selectedCities.value = selectedCities.value.filter(city => city !== cityToRemove);
  // 从 futureWeatherInfo 中移除该城市的数据
  if (futureWeatherInfo.value[cityToRemove]) {
    delete futureWeatherInfo.value[cityToRemove];
  }
};

// 替换城市
const replaceCity = async () => {
  if (cityToAdd.value && !selectedCities.value.includes(cityToAdd.value)) {
    if (selectedCities.value.length < 5) {
      selectedCities.value.push(cityToAdd.value);
    } else {
      selectedCities.value[4] = cityToAdd.value;
    }
    await getCityWeather(cityToAdd.value); // 获取新选择城市的天气信息
    await getFutureWeather(cityToAdd.value); // 获取未来天气数据
  }
  cityToAdd.value = ''; // 重置下拉选择器
};

// 选择省份
const selectProvince = async (provinceName: string) => {
  selectedProvince.value = provinceName;
  console.log(`省份已选中: ${provinceName}`);
  await getCityList(provinceName);
  for (let city of selectedCities.value) {
    await getCityWeather(city); // 传入城市名称,获取当前天气数据
    await getFutureWeather(city); // 获取未来天气数据
  }
};

// 计算天气频率
function calculateWeatherFrequency() {
  let frequencyMap: Record<string, number> = {};

  for (let city of selectedCities.value) {
    let forecasts = futureWeatherInfo.value[city];  // 获取该城市的未来天气数据
    if (forecasts) {
      for (let forecast of forecasts) {
        let weather = forecast.dayWeather;  // 获取天气现象
        if (weather in frequencyMap) {
          frequencyMap[weather] += 1;  // 增加计数
        } else {
          frequencyMap[weather] = 1;  // 初始化计数
        }
      }
    }
  }

  let total = Object.values(frequencyMap).reduce((sum, current) => sum + current, 0);
  let weatherFrequencyData = [];
  for (let [weather, count] of Object.entries(frequencyMap)) {
    weatherFrequencyData.push({ name: weather, value: (count / total * 100).toFixed(2) });
  }
  weatherFrequency.value = weatherFrequencyData;
}

// 初始化折线图
const initChart = async () => {
  if (chartContainer.value) {
    myChart = echarts.init(chartContainer.value);
    await selectProvince(selectedProvince.value);// 等待所有城市的天气数据被获取

    // 使用响应式数据来动态更新图表
    const option = {
      title: {
        text: '夜晚温度折线图'
      },
      tooltip: {
        trigger: 'axis'
      },
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
      },
      toolbox: {
        feature: {
        saveAsImage: {}
        }
      },
      xAxis: {
        data: ['今天', '明天', '后天', '大后天']
      },
      yAxis: {  
        type: 'value'
      },
      legend: {
        data: selectedCities.value
      },
      // 更新系列数据
      series: selectedCities.value.map(city => ({
        name: city,
        type: 'line',
        data: futureWeatherInfo.value[city].map(info => info.nightTemp)
      }))
    };
        myChart.setOption(option);
  }
};

// 更新折线图
const updateChart = () => {
  if (myChart && futureWeatherInfo.value) {
    const seriesData = selectedCities.value.map(city => {
      const cityData = futureWeatherInfo.value[city];
      if (cityData && cityData.length) {
        return {
          name: city,
          type: 'line',
          data: cityData.map(info => info.nightTemp) // 确保使用正确的属性
        };
      } else {
        // 如果数据不存在，提供一个空的数据系列
        return {
          name: city,
          type: 'line',
          data: []
        };
      }
    });

    const option = {
      title: {
        text: '最低温度图'
      },
      tooltip: {
        trigger: 'axis'
      },
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
      },
      toolbox: {
        feature: {
          saveAsImage: {}
        }
      },
      xAxis: {
        data: ['今天', '明天', '后天', '大后天']
      },
      yAxis: {
        type: 'value'
      },
      legend: {
        data: selectedCities.value
      },
      series: seriesData
    };
    myChart.setOption(option, true); // 使用true来使得更新是不合并之前的数据
  }
};

// 初始化最高温度图
const initMaxTempChart = () => {
  if (maxTempChartContainer.value) {
    if (!maxTempChart) {
      maxTempChart = echarts.init(maxTempChartContainer.value);
    }
    const seriesData = selectedCities.value.map(city => {
      const cityData = futureWeatherInfo.value[city];
      if (cityData && cityData.length) {
        return {
          name: city,
          type: 'line',
          data: cityData.map(info => info.dayTemp) // 使用最高温度的属性
        };
      } else {
        // 如果数据不存在，提供一个空的数据系列
        return {
          name: city,
          type: 'line',
          data: []
        };
      }
    });
    
    const option = {
      title: {
        text: '最高温度图'
      },
      tooltip: {
        trigger: 'axis'
      },
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
      },
      toolbox: {
        feature: {
          saveAsImage: {}
        }
      },
      xAxis: {
        data: ['今天', '明天', '后天', '大后天']
      },
      yAxis: {
        type: 'value'
      },
      legend: {
        data: selectedCities.value
      },
      series: seriesData
    };
    maxTempChart.setOption(option, true); // 使用true来使得更新是不合并之前的数据
  }
};

// 计算天气频率
calculateWeatherFrequency();

// 初始化饼图
const initPieChart = () => {
  if (pieChartContainer.value && !pieChart) {
    pieChart = echarts.init(pieChartContainer.value);// 如果 pieChart 实例不存在，初始化它
    const option = {
      title: {
        text: '天气现象频率',
        left: 'center'
      },
      tooltip: {
        trigger: 'item'
      },
      legend: {
        top: '5%',
        left: 'center'
      },
      series: [
    {
      name: '天气及其概率',
      type: 'pie',
      radius: ['40%', '70%'],
      avoidLabelOverlap: false,
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 40,
          fontWeight: 'bold'
        }
      },
      labelLine: {
        show: false
      },
      data: weatherFrequency.value
    }
  ]
    };
    pieChart.setOption(option);
  }else if (pieChart) {
    // 如果 pieChart 实例已经存在，只更新数据
    pieChart.setOption({
      series: [{
        name: '天气及其概率',
        type: 'pie',
        radius: ['40%', '70%'],
        avoidLabelOverlap: false,
        label: {
          show: false,
          position: 'center'
        },
        emphasis: {
          label: {
          show: true,
          fontSize: 40,
          fontWeight: 'bold'
          }
        },
        labelLine: {
          show: false
        },
        data: weatherFrequency.value
      }]
    });
  }
};

// 监听 selectedCities 和 futureWeatherInfo 的变化
watch([selectedCities, futureWeatherInfo], () => {
  calculateWeatherFrequency(); // 在城市选择或天气数据更新时计算频率
  updateChart(); // 更新图表
  initMaxTempChart();
  initPieChart();
}, {
  deep: true // 深度监听对象内部的变化
});

// 组件挂载后执行
onMounted(() => {
  initChart();
  initMaxTempChart();
  calculateWeatherFrequency(); // 确保在组件挂载后计算一次频率
  initPieChart();
});
</script>

<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 220px;
  min-height: 700px;
  overflow-y: auto; /* 允许垂直滚动 */
  max-height: 100vh; /* 设置最大高度 */
  border-radius: 20px;
}
/* 透明化滚动条的样式 */
.el-menu-vertical-demo::-webkit-scrollbar {
  width: 0px; /* 针对 Webkit 浏览器，设置滚动条宽度为0 */
  background: transparent; /* 使滚动条完全透明 */
}

.el-menu-vertical-demo {
  -ms-overflow-style: none; /* 针对 IE 和 Edge, 隐藏滚动条但保持功能 */
  scrollbar-width: none; /* 针对 Firefox, 隐藏滚动条但保持功能 */
}
/* 居中菜单项 */
.el-menu-item {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

/* 如果使用了图标，可能需要对图标和文本进行进一步的布局调整 */
.el-menu-item .el-icon {
  margin-right: 8px; /* 调整图标和文本之间的间距 */
}

/* 主要内容区域*/
.main-content {
  background-color: #cbfad9; 
  padding: 20px;
  min-height: 700px;
  overflow-y: auto; /* 允许垂直滚动 */
  overflow-x: auto;
  max-height: 100vh; /* 设置最大高度 */
  border-radius: 20px;
}

/*右侧边栏*/
.right-sidebar {
  background-color: #63a0fb; 
  padding: 20px;
  min-height: 700px;
  overflow-y: auto; /* 允许垂直滚动 */
  max-height: 100vh; /* 设置最大高度 */
  border-radius: 20px;
  width: 100px;
}
.custom-city-tag {
  width: 100px;
  text-align: center;
  /* 这里可以添加其他你想要的样式，比如背景颜色、字体大小等 */
  -webkit-text-fill-color: aliceblue;
  border: none; /* 移除边框 */
  background-color: transparent; /* 设置背景为透明 */
  font-size: 15px; /* 调整字体大小，根据需要调整 */
  margin-bottom: 20px;
}
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.WeatherCard {
  flex-basis: 200px;
  flex-shrink: 0;
  width: 200px;
  background-color: #75deb8;
  border-radius: 20px;
}
.CityText{
  font-size: 20px;
}
.el-col {
  padding: 4.5px; /* 在这里调整间距大小 */
}
.el-row {
  display: flex;
  align-items: stretch; /* 或者 'center' 根据需要 */
}

.weather-details img { /* 直接针对 img 标签应用样式 */
  width: 80px;
  height: 80px;
  object-fit: contain; /* 确保图像保持纵横比 */
}

.weather-details {
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.temperature-humidity {
display: flex;
flex-direction: column;
align-items: flex-start;
}

.chart-container {
  width: 600px;
  height: 200px;
}
.pie-chart-container {
  width: 400px; 
  height: 400px; 
}
</style>