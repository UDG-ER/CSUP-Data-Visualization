<template>
  <div class="dashboard">
    <devices-info-block
      :devices="devices"
      :selected="selectedDevice"
      :changeDevice="onChangeDevice"
    />
    <devices-charts :measurements="measurements" :changeRange="onChangeRange" />
  </div>
</template>

<script>
import config from "../../config.json";
import DevicesCharts from "./DevicesCharts";
import DevicesInfoBlock from "./DevicesInfoBlock";

export default {
  name: "dashboard",
  components: {
    DevicesCharts,
    DevicesInfoBlock
  },

  data() {
    return {
      devices: false,
      selectedDevice: false,
      selectedRange: false,
      measurements: false
    };
  },
  methods: {
    onChangeDevice(device) {
      if (device === this.selectedDevice) {
        this.selectedDevice = false;
        this.measurements = false;
      } else {
        this.selectedDevice = device;
        this.measurements = false;
      }

      this.updateData();
    },
    onChangeRange(range) {
      this.selectedRange = range;
      this.updateData();
    },
    updateData() {
      if(this.selectedDevice && this.selectedRange){
        this.getDeviceMeasurements();
      }
    },
    getDevices: async function() {
      const getDevicesURL = config.api_url + "/api/Demeter/irrigdevices";

      try {
        const response = await fetch(getDevicesURL, {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
            Authorization: "Bearer " + localStorage.getItem("jwt")
          }
        });
        const result = await response.json();
        setTimeout(() => {
          this.devices = result.IrrigDevices;
        }, 1000);
      } catch (error) {
        console.log("Error with getting irrig devices:" + error);
      }
    },
    getDeviceMeasurements: async function() {
      const getMeasurementsURL =
        config.api_url +
        `/api/Demeter/irrighistorydata?ids=${this.selectedDevice}&startDate=${
          this.selectedRange.substring(0, 10)
        }&endDate=${this.selectedRange.substring(14)}`;

      let device = this.devices.find(d => d.ID === this.selectedDevice)

      try {
        const response = await fetch(getMeasurementsURL, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
            Authorization: "Bearer " + localStorage.getItem("jwt")
          }
        });
        const result = await response.json();
        let labels = result[0].measurements.map(
          measurement => measurement.date
        );
        let datasets = result[0].measurements.map(
          measurement => measurement.value
        );
        this.measurements = {labels, datasets: [{ label: device.DeviceName, data: datasets, backgroundColor: 'rgba(46, 132, 224, 0.6)', borderColor: 'transparent', pointRadius: 0, pointHitRadius: 3 }],  }
        console.log(this.measurements)
      } catch (error) {
        console.log("Error with getting irrig devices:" + error);
      }
    }
  },
  mounted: function() {
    this.getDevices();
  }
};
</script>

<style lang="scss">
.row-equal .flex {
  .va-card {
    height: 100%;
  }
}
.dashboard {
  .va-card {
    margin-bottom: 0 !important;
  }
}
</style>
