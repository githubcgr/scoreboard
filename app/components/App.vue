<template>
  <Page>
    <ActionBar title="Table Tenis Scoreboard" backgroundColor="#3498db" />

    <ScrollView orientation="vertical">
      <StackLayout backgroundColor="#34495e">
        <FlexboxLayout flexDirection="column">
          <GridLayout columns="50, 50, 50, *, 50, 50, 50" rows="auto">
            <Button text="+" backgroundColor="#43b883" @tap="onButtonTap('+', 1)" col="0" row="0" />
            <Button text="-" backgroundColor="#3498db" @tap="onButtonTap('-', 1)" col="2" row="0" />
            <Label :text="total1" col="1" color="white" fontSize="36" textAlignment="center" />

            <GridLayout columns="*" rows="50" col="3" width="200">
              <Button text="Novo Jogo" col="0" row="0" @tap="resetGame" backgroundColor="#ecf0f1" />
            </GridLayout>
            <!-- <Label col="4" text="aa" /> -->

            <Label :text="total2" col="5" color="white" fontSize="36" textAlignment="center" />
            <Button text="+" backgroundColor="#43b883" @tap="onButtonTap('+', 2)" col="6" row="0" />
            <Button text="-" backgroundColor="#3498db" @tap="onButtonTap('-', 3)" col="4" row="0" />
          </GridLayout>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
          <GridLayout columns="100%, *, 100%" width="90%" rows="50, 75, 75, 50" alignSelf="center">

            <GridLayout col="1" row="1" columns="*, *" width="100%" rows="*" alignSelf="center">
              <Button text="Jogador 1" color="#ecf0f1" @tap="setServer(0)" backgroundColor="#0059A4" borderColor="#ecf0f1" borderWidth="2" col="0" row="0" />
              <Button text="Jogador 3" color="#ecf0f1" @tap="setServer(2)" backgroundColor="#0059A4" borderColor="#ecf0f1" borderWidth="2" col="1" row="0" />
            </GridLayout>

            <GridLayout col="1" row="2" columns="*, *" width="100%" rows="*" alignSelf="center">
              <Button text="Jogador 2" color="#ecf0f1" @tap="setServer(1)" backgroundColor="#0059A4" borderColor="#ecf0f1" borderWidth="2" col="0" row="0" />
              <Button text="Jogador 4" color="#ecf0f1" @tap="setServer(3)" backgroundColor="#0059A4" borderColor="#ecf0f1" borderWidth="2" col="1" row="0" />
            </GridLayout>

            <Image
              stretch="aspectFit"
              height="40"
              src="~/assets/images/raquete.png"
              :visibility="stateServe[0]"
              col="0"
              row="1"
              marginRight="5"
            />
            <Image
              stretch="aspectFit"
              height="40"
              src="~/assets/images/raquete.png"
              :visibility="stateServe[1]"
              col="0"
              row="2"
              marginRight="5"
            />

            <Image
              stretch="aspectFit"
              height="40"
              src="~/assets/images/raquete.png"
              :visibility="stateServe[2]"
              col="2"
              row="1"
              marginLeft="5"
            />
            <Image
              stretch="aspectFit"
              height="40"
              src="~/assets/images/raquete.png"
              :visibility="stateServe[3]"
              col="2"
              row="2"
              marginLeft="5"
            />
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
      stateServe: ["hidden", "hidden", "hidden", "visible"],
      server: 3,
      firstToServe: 3,
      orderOfServe: {
        0: [3, 1, 2, 0],
        1: [2, 0, 3, 1],
        2: [1, 3, 0, 2],
        3: [0, 2, 1, 3]
      }
    };
  },
  watch: {
    sumOfPoints: function() {
      let numberOfServes = 2;
      if (this.total1 >= 10 && this.total2 >= 10) {
        numberOfServes = 1;
      }

      if (this.sumOfPoints % numberOfServes == 0) {
        let order = this.orderOfServe[this.firstToServe].indexOf(this.server);
        let n = order+1;
        let next =  this.orderOfServe[this.firstToServe][n];

        if (typeof this.orderOfServe[this.firstToServe][next] == "undefined") {
          this.server = this.orderOfServe[this.firstToServe][0];
        } else {
          this.server = next;
        }
      }
    },
    server: function() {
      this.stateServe = ["hidden", "hidden", "hidden", "hidden"];

      for (let i = 0; i <= 3; i++) {
        if (this.server == i) {
          this.stateServe[i] = "visible";
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
    },
    resetGame: function() {
      this.total1 = 0;
      this.total2 = 0;
      this.sumOfPoints = 0;
    },
    setServer: function (serverPosition) {
      this.server = serverPosition;
      
      if (this.sumOfPoints == 0) {
        this.firstToServe = serverPosition;
      }
    }
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #3498db;
  color: #ffffff;
}
.color1 {
  color: #ecf0f1;
}
.border-color1{
  border-color: #ecf0f1
}

</style>
