<template>
  <div id="app">
    <div class="circle-cursor circle-cursor--inner"></div>
    <canvas class="circle-cursor circle-cursor--outer" resize></canvas>
    <div id="nav">
      <div class="nav-wrap">
        <router-link to="/" class="nav-link">
          <span>Home</span>
        </router-link>
      </div>
      <div class="nav-wrap">
        <router-link to="/about" class="nav-link">
          <span>About</span>
        </router-link>
      </div>
      <div class="nav-wrap">
        <router-link to="/about" class="nav-link">
          <span>Contact</span>
        </router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  mounted() {
    
    (function () {

      const link = document.querySelectorAll('.nav-wrap > .nav-link');
      const cursor = document.querySelector('.cursor');

      const animateit = function (e) {
            const span = this.querySelector('.nav-wrap .nav-link span');
            const { offsetX: x, offsetY: y } = e,
            { offsetWidth: width, offsetHeight: height } = this,

            move = 25,
            xMove = x / width * (move * 2) - move,
            yMove = y / height * (move * 2) - move;

            span.style.transform = `translate3d(${xMove}px, ${yMove}px, 0)`;

            if (e.type === 'mouseleave') span.style.transform = '';
      };

      const editCursor = e => {
            const { clientX: x, clientY: y } = e;
            cursor.style.left = x + 'px';
            cursor.style.top = y + 'px';
      };

      link.forEach(b => b.addEventListener('mousemove', animateit));
      link.forEach(b => b.addEventListener('mouseleave', animateit));
      window.addEventListener('mousemove', editCursor);

    })();
  }
}
</script>

<style lang="scss">
@import 'src/assets/css/_main.scss';
</style>
