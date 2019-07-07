<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />

    <GridLayout columns="115, 115" rows="115, 115">
      <FlexboxLayout row=0 column=0 alignItems="flex-start" backgroundColor="#3c495e">
        <Button
          text="+"
          width="10%"
          height="70"
          backgroundColor="#43b883"
          @tap="onButtonTap('+', 1)"
        />
        <Button
          text="-"
          width="10%"
          height="70"
          backgroundColor="#1c6b48"
          @tap="onButtonTap('-', 1)"
        />
        <Label width="30%" height="70" fontSize="36" class="colorWhite">{{ total1 }}</Label>
        <Label
          textWrap="true"
          width="30%"
          height="70"
          class="alignRight colorWhite"
          fontSize="36"
        >{{ total2 }}</Label>
        <Button
          text="+"
          width="10%"
          height="70"
          backgroundColor="#43b883"
          @tap="onButtonTap('+', 2)"
        />
        <Button
          text="-"
          width="10%"
          height="70"
          backgroundColor="#1c6b48"
          @tap="onButtonTap('-', 2)"
        />
      </FlexboxLayout>

      <FlexboxLayout alignItems="flex-end">
        <Button
          text="+"
          width="10%"
          height="70"
          backgroundColor="#43b883"
          @tap="onButtonTap('+', 1)"
        />
        <Button
          text="-"
          width="10%"
          height="70"
          backgroundColor="#1c6b48"
          @tap="onButtonTap('-', 1)"
        />
        <Label width="30%" height="70" fontSize="36" class="colorWhite">{{ total1 }}</Label>
        <Label
          textWrap="true"
          width="30%"
          height="70"
          class="alignRight colorWhite"
          fontSize="36"
        >{{ total2 }}</Label>
        <Button
          text="+"
          width="10%"
          height="70"
          backgroundColor="#43b883"
          @tap="onButtonTap('+', 2)"
        />
        <Button
          text="-"
          width="10%"
          height="70"
          backgroundColor="#1c6b48"
          @tap="onButtonTap('-', 2)"
        />
      </FlexboxLayout>
    </GridLayout>
  </Page>
</template>

<script >
export default {
  data() {
    return {
      total1: 3,
      total2: 0
    };
  },
  methods: {
    onButtonTap: function(type, team) {
      if (type == "-") {
        if (team == 1) {
          this.total1--;
        } else {
          this.total2--;
        }
      } else {
        if (team == 1) {
          this.total1++;
        } else {
          this.total2++;
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
