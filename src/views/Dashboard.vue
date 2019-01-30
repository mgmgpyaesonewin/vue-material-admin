<template>
  <div id="pageDashboard">
    <v-container grid-list-xl fluid>
      <p class="subheading">Restaurant Status</p>
      <v-layout row wrap>
        <!-- mini chart start -->
        <v-flex lg3 sm6>
          <v-card>
            <v-card-text>
              <div class="layout row ma-0 align-center justify-space-between">
                <div class="text-box">
                  <div class="subheading pb-2">Sign Up</div>
                  <span class="grey--text">
                    10%
                    <v-icon small color="green">trending_up</v-icon>
                  </span>
                </div>
                <div class="chart">
                  <v-progress-circular
                    :size="60"
                    :width="5"
                    :rotate="270"
                    :value="10"
                    color="success"
                  >
                    10
                  </v-progress-circular>
                </div>
              </div>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex lg3 sm6>
          <v-card>
            <v-card-text>
              <div class="layout row ma-0 align-center justify-space-between">
                <div class="text-box">
                  <div class="subheading pb-2">Promotions</div>
                  <span class="grey--text">
                    25%
                    <v-icon small color="pink">trending_up</v-icon>
                  </span>
                </div>
                <div class="chart">
                  <v-progress-circular
                    :size="60"
                    :width="5"
                    :rotate="270"
                    :value="25"
                    color="pink"
                  >
                    25
                  </v-progress-circular>
                </div>
              </div>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex lg3 sm6>
          <v-card>
            <v-card-text>
              <div class="layout row ma-0 align-center justify-space-between">
                <div class="text-box">
                  <div class="subheading pb-2">Opening Now</div>
                  <span class="grey--text">
                    10%
                    <v-icon small color="primary">fa fa-cutlery</v-icon>
                  </span>
                </div>
                <div class="chart">
                  <v-progress-circular
                    :size="60"
                    :width="5"
                    :rotate="270"
                    :value="10"
                    color="primary"
                  >
                    10
                  </v-progress-circular>
                </div>
              </div>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex lg3 sm6>
          <v-card>
            <v-card-text>
              <div class="layout row ma-0 align-center justify-space-between">
                <div class="text-box">
                  <div class="subheading pb-2">Logged On</div>
                  <span class="grey--text">
                    -25%
                    <v-icon small color="warning">trending_down</v-icon>
                  </span>
                </div>
                <div class="chart">
                  <v-progress-circular
                    :size="60"
                    :width="5"
                    :rotate="-180"
                    :value="25"
                    color="warning"
                  >
                    - 25
                  </v-progress-circular>
                </div>
              </div>
            </v-card-text>
          </v-card>
        </v-flex>
        <!-- mini chart end -->

        <!-- mini statistic start -->
        <v-flex lg6 sm6 xs12>
          <linear-statistic
            title="Sales"
            sub-title="Sales increase"
            icon="trending_up"
            color="success"
            :value="15"
          >
          </linear-statistic>
        </v-flex>
        <v-flex lg6 sm6 xs12>
          <linear-statistic
            title="Orders"
            sub-title="Increase"
            icon="fa fa-tasks"
            color="pink"
            :value="30"
          >
          </linear-statistic>
        </v-flex>
        <!-- mini statistic  end -->
        <v-flex lg6 sm12 xs12>
          <v-widget title="Driver Status" content-bg="white">
            <div slot="widget-content">
              <e-chart
                :path-option="[
                  ['dataset.source', driversStatusData],
                  ['legend.bottom', '0'],
                  ['color', [color.lightBlue.base, color.indigo.base, color.pink.base, color.green.base, color.cyan.base, color.teal.base]],
                  ['legend.orient', 'horizontal'],
                  ['legend.y', 'bottom'],
                  ['xAxis.show', false],
                  ['yAxis.show', false],
                  ['series[0].type', 'pie'],
                ]"
                height="400px"
                width="100%"
              >
              </e-chart>
            </div>
          </v-widget>
        </v-flex>
        <v-flex lg6 sm12 xs12>
          <v-widget title="Summary">
            <div slot="widget-content">
                <e-chart 
                :path-option="[
                  ['dataset.source', dataset.summary],
                  ['color', [color.amber.base, color.indigo.base, color.pink.base, color.green.base, color.teal.base, color.purple.base, color.brown.base, color.amber.base]],
                  ['legend.orient', 'horizontal'],
                  ['legend.y', 'bottom'],
                  ['xAxis.show', false],
                  ['yAxis.show', false],
                  ['series[0].type', 'pie'],
                  ['series[0].avoidLabelOverlap', true],
                  ['series[0].radius', ['50%', '70%']],
                ]"
                height="400px"
                width="100%"
                >
                </e-chart>   
            </div>
          </v-widget>            
        </v-flex>
        <!-- Circle statistic -->
        <v-flex lg4 sm12 xs12>
          <circle-statistic
            title="Summary"
            sub-title="(+ 67%)"
            caption="67 order received"
            icon="fa fa-list-ol"
            color="info"
            value="67"
          >
          </circle-statistic>
        </v-flex>
        <v-flex lg8 sm12 xs12>
          <plain-table-order></plain-table-order>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import API from "@/api";
import { summaryData } from "@/api/summary";
import EChart from '@/components/chart/echart';
import MiniStatistic from '@/components/widgets/statistic/MiniStatistic';
import PostListCard from '@/components/widgets/card/PostListCard';
import ProfileCard from '@/components/widgets/card/ProfileCard';
import PostSingleCard from '@/components/widgets/card/PostSingleCard';
import WeatherCard from '@/components/widgets/card/WeatherCard';
import PlainTable from '@/components/widgets/list/PlainTable';
import PlainTableOrder from '@/components/widgets/list/PlainTableOrder';
import VWidget from '@/components/VWidget';
import Material from 'vuetify/es5/util/colors';
import VCircle from '@/components/circle/VCircle';
import BoxChart from '@/components/widgets/chart/BoxChart';
import ChatWindow from '@/components/chat/ChatWindow';
import CircleStatistic from '@/components/widgets/statistic/CircleStatistic';
import LinearStatistic from '@/components/widgets/statistic/LinearStatistic';
export default {
  components: {
    VWidget,
    MiniStatistic,
    ChatWindow,
    VCircle,
    WeatherCard,
    PostSingleCard,
    PostListCard,
    ProfileCard,
    EChart,
    BoxChart,
    CircleStatistic,
    LinearStatistic,
    PlainTable,
    PlainTableOrder    
  },
  data: () => ({
    color: Material,
    selectedTab: 'tab-1',
    dataset: {
      summary: summaryData
    }
  }),
  computed: {
    activity () {
      return API.getActivity();
    },
    posts () {
      return API.getPost(3);
    },
    siteTrafficData() {
      return API.getMonthVisit;
    },
    driversStatusData() {
      return API.getDriversStatus;
    }
  }
};
</script>
