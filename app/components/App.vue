<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />

    <ScrollView orientation="vertical">
      <StackLayout backgroundColor="#3c495e">
        <FlexboxLayout flexDirection="column">
          <GridLayout columns="50, 50, 50, *, 50, 50, 50" rows="auto">
            <Button text="+" backgroundColor="#43b883" @tap="onButtonTap('+', 1)" col="0" row="0" />
            <Button text="-" backgroundColor="#1c6b48" @tap="onButtonTap('-', 1)" col="2" row="0" />
            <Label :text="total1" col="1" color="white" fontSize="36" textAlignment="center" />

            <Label col="4" />

            <Label :text="total2" col="5" color="white" fontSize="36" textAlignment="center" />
            <Button text="+" backgroundColor="#43b883" @tap="onButtonTap('+', 2)" col="6" row="0" />
            <Button text="-" backgroundColor="#1c6b48" @tap="onButtonTap('-', 3)" col="4" row="0" />
          </GridLayout>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
          <GridLayout columns="50, 150, 50" rows="50, 50, 50, 50">
            <Label text="1" :backgroundColor="colorServe[0]" col="0" row="1" />
            <Label text="2" :backgroundColor="colorServe[1]" col="0" row="2" />
            
            <Label col="1" backgroundColor="black" rowSpan="2" row="1" />

            <Label text="3" :backgroundColor="colorServe[2]" col="2" row="1" />
            <Label text="4" :backgroundColor="colorServe[3]" col="2" row="2" />
          </GridLayout>
        </FlexboxLayout>
      </StackLayout>
    </ScrollView>
  </Page>
</template>

<script >
export default {
  data() {
    return {
      total1: 0,
      total2: 0,
      sumOfPoints: 0,
      colorServe: ["#ddd", "#ddd", "#ddd", "#43b883"],
      server: 3
    };
  },
  watch: {
    sumOfPoints: function() {
      if (this.sumOfPoints % 2 == 0) {
        if (this.server == 3) {
          this.server = 0;
        } else if (this.server == 0) {
          this.server = 2;
        } else if(this.server == 2){
          this.server = 1;
        } else {
          this.server = 3;
        }
      }
    },
    server: function() {
      this.colorServe = ["#ddd", "#ddd", "#ddd", "#ddd"];
      
      for (let i = 0; i <= 3; i++) {
        if (this.server == i) {
          this.colorServe[i] = "#43b883";
        }
      }
      
    }
  },
  methods: {
    onButtonTap: function(type, team) {
      if (type == "-") {
        if (team == 1) {
          this.total1--;
          this.sumOfPoints--;
        } else {
          this.total2--;
          this.sumOfPoints--;
        }
      } else {
        if (team == 1) {
          this.total1++;
          this.sumOfPoints++;
        } else {
          this.total2++;
          this.sumOfPoints++;
        }
      }
    }
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
.alignRight {
  text-align: right;
}
.colorWhite {
  color: #fff;
}
</style>
