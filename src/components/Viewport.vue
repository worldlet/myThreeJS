<script setup>

</script>

<template>
  <div class="dashboard">
    <div class="header">header</div>
    <div class="center">header</div>
    <div class="icon">
      <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M4 19v-9q0-.475.213-.9t.587-.7l6-4.5q.525-.4 1.2-.4t1.2.4l6 4.5q.375.275.588.7T20 10v9q0 .825-.588 1.413T18 21h-3q-.425 0-.712-.288T14 20v-5q0-.425-.288-.712T13 14h-2q-.425 0-.712.288T10 15v5q0 .425-.288.713T9 21H6q-.825 0-1.412-.587T4 19Z"></path></svg>
    </div>
<!--    <div class="item-1"><h2>header</h2></div>
    <div class="item-2"><h2>模块1</h2></div>
    <div class="item-3"><h2>模块2</h2></div>
    <div class="item-4"><h2>模块3</h2></div>
    <div class="item-5"><h2>模块4</h2></div>
    <div class="item-6"><h2>模块5</h2></div>
    <div class="item-7"><h2>模块6</h2></div>
    <div class="item-8"><h2>模块7</h2></div>
    <div class="item-9"><h2>模块8</h2></div>-->
  </div>
</template>

<style lang="scss" scoped>
.dashboard {
  display: grid;
  width: 100%;
  height: 100%;
  /* px-to-viewport-ignore-next */
  grid-template-columns: [c1] minmax(100px, 1fr) [c2] 2fr [c3] minmax(100px, 1fr) [c4];
  /* px-to-viewport-ignore-next */
  grid-template-rows: [r1] 8% [r2] 28% [r3] auto [r4] 28% [r5];
  //row-gap: 20px;     // 行间距
  //column-gap: 20px;  // 列间距
  gap: 16px;   // 行列间距
  grid-template-areas: "a a a"
                       "b c d"
                       "e c f"
                       "g h i";

  .header {
    //grid-column-start: 2;
    //grid-column-end: 4;
    grid-column-end: span 3;
    background: #eeeeee;
  }

  .center {
    grid-area: c;
    background: #ddfbff;
  }

  h2 {
    font-size: 16px;
    font-weight: bold;
  }

  .item-3 {
    //grid-column-start: 2;
    //grid-column-end: 3;
    grid-column: 2 / 3;
    //grid-row-start: 2;
    //grid-row-end: 4;
    grid-row: 2 / 4;
  }
}



h1 {
  position: relative;
  /* px-to-viewport-ignore-next */
  width: 200px;
  height: 80px; /* px-to-viewport-ignore */
  color: #0a6cff;
  font-size: 28px;

  &:after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    border-top: 1px solid #666;
    transform: scaleY(0.5);
  }
}
</style>