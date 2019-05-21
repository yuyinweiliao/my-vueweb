
<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="bg-grey-10 text-white" dark style="height:50px">
      <div class="row">
        <div class="col">
          <!-- <img src="statics/logo-default.png" style="width: 130px; height: 44px"> -->
        </div>
        <div class="col"></div>
        <div class="col">
          <q-btn
            unelevated
            class="absolute-right q-mr-sm bg-red-4"
            style="height:40px;margin-top:5px;margin-right:20px"
            label="释放设备"
          />
        </div>
      </div>
    </q-header>
    <q-page-container>
      <q-splitter
        v-model="splitterLeft"
        :limits="[25, 60]"
        :style="'height:'+Math.floor(leftHeight)+'px'"
        separator-class="bg-gray"
        separator-style="width: 3px"
      >
        <template v-slot:before>
          <div dark class="absolute-center bg-grey-4" id="left" ref="left" :style="leftStyle">
            <canvas ref="canvasfz" id="canvasfz" 
            :style="'height:'+Math.floor(leftHeight-72)+'px'" />
            <canvas ref="canvas" id="canvas" 
            :style="'height:'+Math.floor(leftHeight-72)+'px'" />
            <span ref="finger" class="finger finger-0" :style="fingerstyle" />
            <div class="bg-grey-10 text-white absolute-top">
              <q-bar dark class="bg-grey-6 text-white">
                <label>{{dInfo}}</label>
                <q-space/>
                <q-btn
                  flat
                  dense
                  :style="'width:30px'"
                  class="q-mr-sm"
                  icon="stay_primary_landscape"
                />
                <q-btn
                  flat
                  dense
                  :style="'width:30px'"
                  class="q-mr-sm"
                  icon="stay_primary_portrait"
                />
                <q-btn flat dense :style="'width:30px'" class="q-mr-sm" icon="remove_red_eye"/>
              </q-bar>
            </div>
            <!--stay_primary_landscape stay_primary_portrait  backspance  <canvas ref="canvas" :height="imgHeight" v-bind:width="imgWidth"></canvas>-->

            <div>
              <q-bar class="bg-grey-8 text-white absolute-bottom">
                <q-btn flat dense icon="menu" :style="'width:25%'" class="q-mr-sm"/>
                <q-btn flat dense icon="home" :style="'width:25%'" class="q-mr-sm"/>
                <q-btn flat dense icon="crop_free" :style="'width:25%'" class="q-mr-sm"/>
                <q-btn flat dense icon="reply" :style="'width:25%'" class="q-mr-sm"/>
              </q-bar>
            </div>
          </div>
        </template>
        <template v-slot:separator>
          <q-avatar color="grey-6" text-color="white" size="20px" icon="drag_indicator"/>
        </template>
        <template v-slot:after>
          <q-splitter
            v-model="splitterFoot"
            separator-class="bg-gray"
            separator-style="height: 3px"
            :limits="[60, 90]"
            horizontal
          >
            <template v-slot:before>
              <div>
                <q-splitter
                  v-model="splitterRight"
                  :limits="[60, 90]"
                  :style="'height:'+Math.floor((leftHeight-5)*splitterFoot/100)+'px'"
                  separator-class="bg-gray"
                  separator-style="width: 3px"
                >
                  <template v-slot:before>
                    <div class="q-pa-md">
                      <div class="text-h4">center</div>
                      <div
                        v-for="n in 20"
                        :key="n"
                        class="q-my-md"
                      >{{ n }}. {{splitterFoot}}Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quis praesentium cumque magnam odio iure quidem, quod illum numquam possimus obcaecati commodi minima assumenda consectetur culpa fuga nulla ullam. In, libero.</div>
                    </div>
                  </template>
                  <template v-slot:separator>
                    <q-avatar color="grey-6" text-color="white" size="20px" icon="code"/>
                  </template>
                  <template v-slot:after>
                    <div class="q-pa-md">
                      <div class="text-h4">right</div>
                      <div
                        v-for="n in 20"
                        :key="n"
                        class="q-my-md"
                      >{{ n }}. Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quis praesentium cumque magnam odio iure quidem, quod illum numquam possimus obcaecati commodi minima assumenda consectetur culpa fuga nulla ullam. In, libero.</div>
                    </div>
                  </template>
                </q-splitter>
              </div>
            </template>
            <template v-slot:separator>
              <q-avatar color="grey-6" text-color="white" size="20px" icon="unfold_more"/>
            </template>
            <template v-slot:after>
              <div id="footer" class="bg-grey-10 text-white">
                <q-tabs
                  v-model="tab"
                  dense
                  dark
                  align="left"
                  class="bg-grey-10 text-gery-9 shadow-2"
                  :breakpoint="0"
                >
                  <q-tab name="mails" label="输出"></q-tab>
                  <q-tab name="alarms" label="日志"></q-tab>
                  <q-tab name="movies" label="截图"></q-tab>
                </q-tabs>

                <q-tab-panels
                  v-model="tab"
                  dark
                  class="bg-grey-9 text-white"
                  :style="'height:'+Math.floor((leftHeight-5)*(100-splitterFoot)/100 -36)+'px'"
                  animated
                >
                  <q-tab-panel name="mails">
                    <div class="text-h6">Mails</div>Lorem ipsum dolor sit amet consectetur adipisicing elit.
                  </q-tab-panel>
                  <q-tab-panel name="alarms">
                    <div class="text-h6">Alarms</div>Lorem ipsum dolor sit amet consectetur adipisicing elit.
                  </q-tab-panel>
                  <q-tab-panel name="movies">
                    <div class="text-h6">Movies</div>Lorem ipsum dolor sit amet consectetur adipisicing elit.
                  </q-tab-panel>
                </q-tab-panels>
              </div>
            </template>
          </q-splitter>
        </template>
      </q-splitter>
    </q-page-container>
  </q-layout>
</template>


<script>
export default {
  name: "MyLayout",
  data() {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      left: true,
      right: true,
      splitterLeft: 30, // start at 50%
      splitterRight: 62, // start at 60%
      splitterFoot: 80,
      tab: "mails",
      screenWidth: window.innerWidth,
      screenHeight: window.innerHeight,
      leftHeight: window.innerHeight - 50,
      leftWidth: 300,
      isconnect: false,
      imgHeight: 500,
      imgWidth: 200,
      ctx: null,
      canvas: null,
      gctx:null,
      canvasfz: null,
      wsimg: null,
      websock: null,
      nodes: null,
      cursor: {},
      swipeStartPoint: {},
      showCursorPercent: true,
      fingerstyle: "",
      dInfo: "127.0.0.1"
    };
  },
  created() {
    // 
    this.loadMinicap();
    
  },
  destroyed() {
    this.websock.close(); //离开路由之后断开websocket连接
  },
  watch: {
    // //监听屏幕变化
    screenWidth: function(val) {
      this.refreshScreen();
    },
    screenHeight: function() {
      this.refreshScreen();
    }
  },
  mounted() {
    var self = this;
    this.canvas = this.$refs.canvas;
    this.gctx=this.canvas.getContext('2d');
    this.canvasfz = this.$refs.canvasfz;
    this.wsimg = this.$refs.wsimg;
    this.ctx = self.canvas.getContext("2d");
    this.activeMouseControl();

    window.onresize = () => {
      return (() => {
        this.refreshScreen();
      })();
    };
  },
  methods: {
    loadMinicap: function() {
      var self=this;
      var id="866402033914525";
      var url="http://10.13.43.215:7100/api/v1/devices/"+id;
      var url="http://10.13.43.215/matlab/query/mtt/proxy.php?method=deviceInfo&account=yuhuahuan&token=852091&dev_id="+id+"&type=1"
      this.$axios
        .get(url)
        .then((response) => {
          var data= response.data;
          self.dInfo=data.result.stf.display.url
          console.log(self.dInfo);
          self.initWebSocket(self.dInfo);
        })
        .catch(() => {
          this.$q.notify({
            color: "negative",
            position: "top",
            message: "Loading failed",
            icon: "report_problem"
          });
        });
    },
    checkVersion: function() {
      var self = this;
      $.ajax({
        url: LOCAL_URL + "api/v1/version",
        type: "GET"
        //contentType: "application/json; charset=utf-8"
      })
        .done(function(ret) {
          console.log("version", ret.name);
          if (ret.name !== LOCAL_VERSION) {
            self.showError(
              "Expect local server version: " +
                LOCAL_VERSION +
                " but got " +
                ret.name +
                ", Maybe you need upgrade 'weditor'"
            );
            return;
          }
          // var lastScreenshotBase64blob = localStorage.screenshotBase64blob;
          // if (lastScreenshotBase64blob) {
          //   self.drawBlobImageToScreen(lastScreenshotBase64blob);
          //   self.canvasStyle.opacity = 1.0;
          // }
          // var lastScreenshotBase64 = localStorage.screenshotBase64;
          // if (lastScreenshotBase64) {
          //   var blob = b64toBlob(lastScreenshotBase64, 'image/jpeg');
          //   self.drawBlobImageToScreen(blob);
          //   self.canvasStyle.opacity = 1.0;
          // }
          // if (localStorage.windowHierarchy) {
          //   // self.originNodes = JSON.parse(localStorage.windowHierarchy);
          //   var source = JSON.parse(localStorage.windowHierarchy);
          //   self.drawAllNodeFromSource(source);
          //   self.loading = false;
          //   self.canvasStyle.opacity = 1.0;
          // }
        })
        .fail(function(ret) {
          self.showError(
            "<p>Local server not started, start with</p><pre>$ python -m weditor</pre>"
          );
        })
        .always(function() {
          self.loading = false;
        });
    },
    disConnect: function() {
      if (this.isconnect) {
        this.isconnect = false;
        this.clearCanvasRect();
        var ws = new WebSocket("ws://" + this.deviceUrl + ":7912/minicap");
        ws.onclose = function() {
          //console.log('onclose', arguments)
        };
        ws.onerror = function() {
          console.log("onerror", arguments);
        };
        ws.onmessage = function(message) {
          ws.close();
        };
        ws.onopen = function() {
          ws.close();
        };
      }
    },
    doConnect: function() {
      var lastDeviceId = this.deviceId;
      this.deviceId = "";
      return $.ajax({
        url: LOCAL_URL + "api/v1/connect",
        method: "POST",
        data: {
          platform: this.platform,
          deviceUrl: this.deviceUrl
        }
      })
        .then(
          function(ret) {
            // console.log(ret);
            this.deviceId = ret.deviceId;
            this.display.width = ret.displaywidth;
            this.display.height = ret.displayheight;
            this.liveFlag = this.isconnect = true;
            if (this.isconnect) {
              this.loadLiveScreen();
            }
          }.bind(this)
        )
        .fail(
          function(ret) {
            this.liveFlag = this.isconnect = false;
            this.showAjaxError(ret);
            this.deviceId = lastDeviceId;
          }.bind(this)
        );
    },
    keyevent: function(meta) {
      var code = 'iqy.press("' + meta + '")';
      if (this.platform != "Android" && meta == "home") {
        code = "iqy.home()";
      }
      return this.codeRunDebugCode(code).then(
        function() {
          return this.codeInsert(code);
        }.bind(this)
      );
      //.then(this.delayReload)
    },
    refreshScreen() {
      var self = this;
      self.screenWidth = window.innerWidth; // this.$q.screen.width;
      self.leftHeight = window.innerHeight - 50;
      self.leftWidth = Math.floor((self.screenWidth * self.splitterLeft) / 100);
      // console.log(self.screenWidth, self.leftHeight);
      self.leftWidth=self.getLeftWidth();
 
    },
    getLeftWidth(){
      var self = this;
       var leftw = Math.floor((self.screenWidth * self.splitterLeft) / 100) - 2;

      if (leftw < 300) {
        self.splitterLeft = Math.ceil((300 / self.screenWidth) * 100);
        leftw = 300;
      }
    return leftw;
    },
    initWebSocket(wsuri) {
      //初始化weosocket
      // http://10.13.43.215:7100/api/v1/devices/JJNNEI7HBIFYAYGQ
      //http://10.13.43.215:7100/api/v1/devices/1e7c1c50
      // const wsuri = "ws://10.2.41.133:7912/minicap";
      // const wsuri="ws://10.13.43.215:7110/socket.io/?uip=10.13.43.215&EIO=3&transport=websocket";
      // const wsuri="ws://10.13.43.215:7110/socket.io/?uip=10.13.43.215&EIO=3&transport=websocket";
      // const wsuri = "ws://10.3.4.198:7408";
      this.websock = new WebSocket(wsuri);
      this.websock.onmessage = this.websocketonmessage;
      this.websock.onopen = this.websocketonopen;
      this.websock.onerror = this.websocketonerror;
      this.websock.onclose = this.websocketclose;
    },
    convertSwipe: function(strz) {
      if (strz.indexOf(".swipe_left()") > -1) {
        strz = strz.replace(
          /.swipe_left\(\)/g,
          ".swipe(0.8, 0.5, 0.2, 0.5) # swipeleft"
        );
      }
      if (strz.indexOf(".swipe_right()") > -1) {
        strz = strz.replace(
          /.swipe_right\(\)/g,
          ".swipe(0.2, 0.5, 0.8, 0.5) # swiperight"
        );
      }
      if (strz.indexOf(".swipe_up()") > -1) {
        strz = strz.replace(
          /.swipe_up\(\)/g,
          ".swipe(0.5, 0.8, 0.5, 0.2) # swipeup"
        );
      }
      if (strz.indexOf(".swipe_down()") > -1) {
        strz = strz.replace(
          /.swipe_down\(\)/g,
          ".swipe(0.5, 0.2, 0.5, 0.8) # swipedown"
        );
      }
      return strz;
    },
    convertTouch: function(code) {
      var self = this;
      var reg = /iqy\.touch\((.*?)(?=[\)])/g;
      if (code.indexOf("iqy.touch(") > -1) {
        var w = self.display.width;
        var h = self.display.height;
        code.match(reg).map(function(v) {
          var xy = v.replace("iqy.touch(", "");
          //document.write(xy+ "<br />")
          var x = xy.split(",")[0] + "*iqy.device_info['display']['width']";
          var y = xy.split(",")[1] + "*iqy.device_info['display']['height']";
          var newtouch =
            "iqy.touch.down(" +
            x +
            "," +
            y +
            ")\r\ntime.sleep(.01)\r\niqy.touch.up()  # 模拟抬起";
          code = code.replace(v, newtouch);
        });
        return code;
      }
      return code;
    },
    convertCode: function(strz) {
      if (strz.indexOf("iqy.") > -1) {
        strz = strz.replace(/iqy\./g, "d.");
      }
      if (strz.indexOf("iqy(") > -1) {
        strz = strz.replace(/iqy\(/g, "d(");
      }
      return strz;
    },
    convertDisplay: function(script) {
      var self = this;
      script = script.replace(/\*dis_w/g, "*" + self.display.width);
      script = script.replace(/\*dis_h/g, "*" + self.display.height);
      return script;
    },
    //去掉左边的空格
    leftTrim: function(str) {
      return str.replace(/^\s*/g, "");
    },
    //判断是不是注释
    isAnnotation: function(str) {
      str = this.leftTrim(str);
      if (str.length > 1) {
        return str.substr(0, 1) == "#";
      }
      return false;
    },
     doInstall: function (text) {
      if (!text) {
        text = window.prompt("输入http://xxx/xx.apk路径")
      }
      if (!text) {
        return;
      }
      var code = 'iqy.app_install("' + text + '")';
      this.codeInsert(code);
      this.codeRunDebugCode(code);
    },
    doStart: function (text) {
      if (!text) {
        text = window.prompt("输入com.example.xxx")
      }
      if (!text) {
        return;
      }
      var code = 'iqy.app_start("' + text + '")';
      this.codeInsert(code);
      this.codeRunDebugCode(code);
    },
    doStop: function (text) {
      if (!text) {
        text = window.prompt("输入com.example.xxx")
      }
      if (!text) {
        return;
      }
      var code = 'iqy.app_stop("' + text + '")';
      this.codeInsert(code);
      this.codeRunDebugCode(code);
    },
    doSendKeys: function (text) {
      // self.codeInsert()
      if (!text) {
        text = window.prompt("输入字符串");
      }
      if (!text) {
        return;
      }
      var code;
      // var params = ['"' + text + '"']
      if (this.nodeSelected) {
        var params = this.generateNodeSelectorParams(this.nodeSelected);
        code = 'iqy(' + params.join(', ') + ').set_text("' + text + '")';

        // code += "\n" + 'd.press("ENTER")'
      } else {
        code = 'iqy.type("' + text + '")';
      }
      // var code = 'd.type(' + params.join(', ') + ')'
      // this.loading = true;
      this.codeInsert(code);
      this.codeRunDebugCode(code);
      //.then(this.delayReload)
    },

    doClear: function () {
      var code = 'iqy.clear_text()'
      this.codeRunDebugCode(code)
        //.then(this.delayReload)
        .then(function () {
          return this.codeInsert(code);
        }.bind(this))
    },
    clearEditer: function () {
      var self = this;
      self.editor.setValue("");
    },
    doAddEdit: function (node) {
      var self = this;
      var code = this.generatedCode;
      if (code.length > 0) {
        code += ".click()"
        self.codeInsert(code);
      }


    },
    doTap: function (node) {
      var self = this;
      var code = this.generateNodeSelectorCode(node);
      // FIXME(ssx): put into a standalone function
      code += ".click()"
      self.codeInsert(code);
      // this.loading = true;
      this.codeRunDebugCode(code)
        //.then(function () {
        //  self.delayReload();
        //})
        .fail(function () {
          self.loading = false;
        })
    },
    doWait: function (node) {
      var self = this;
      var code = this.generateNodeSelectorCode(node);
      code += ".wait()"
      self.codeInsert(code);
    },
    doAssertExist: function (node) {
      var self = this;
      var code = this.generateNodeSelectorCode(node);
      code = "assert " + code + ".exists()"
      self.codeInsert(code);
    },
    doSleep: function () {
      var self = this
      code = "time.sleep(1)"
      self.codeInsert(code);
    },
    doOneSwipe: function (direction) {
      var self = this;
      // if (this.platform == 'iOS') {
      //   code = "s.swipe_" + direction + "()";
      // } else {
      //   code = "d.swipe_" + direction + "()";
      // }
      code = "iqy.swipe_" + direction + "()";
      code = self.convertSwipe(code);
      self.codeInsert(code);
      // this.loading = true;
      this.codeRunDebugCode(code);
      // .then(function () {
      // //  self.delayReload();
      // })
      // .fail(function () {
      //   self.loading = false;
      // })
    },


    doClick: function (x, y) {
      var code = 'iqy.click(' + x + ', ' + y + ')';
      this.codeInsert(code);
      this.codeRunDebugCode(code);
    },
    doPositionTap: function (x, y) {
      this.doTouch(x, y);
      // var code = 'iqy.click(' + x + ', ' + y + ')';
      // // var code = 'd.click(' + x + ', ' + y + ')';
      // // if (this.platform == 'iOS') {
      // //   code = 's.click(' + x + ', ' + y + ')';
      // // }
      // this.codeInsert(code);
      // this.codeRunDebugCode(code)
      // //.then(this.delayReload)
    },
    doTouch: function (x, y) {
      var self = this;
      var code = 'iqy.touch(' + x + ', ' + y + ')' + ' # 模拟按下';
      this.codeInsert(code);
      this.codeRunDebugCode(code);
    },
    clearCanvasRect: function() {
      var self = this;
      var canvas = self.canvasfz;
      var ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      if (self.nodes) {
        self.nodes.forEach(function(node) {
          if (!node.rect) {
          } else {
            ctx.clearRect(0, 0, node.rect.width, node.rect.height);
          }
        });
      }
    },
    drawAllNode: function() {
      var self = this;
      self.clearCanvasRect();
      if (self.nodes) {
        self.nodes.forEach(function(node) {
          // ignore some types
          if (["Layout"].includes(node.type)) {
            return;
          }
          self.drawNode(node, "black", true);
        });
      }
    },
    drawHoverNode: function(pos) {
      var self = this;
      var canvas = self.canvasfz;
      self.nodeHovered = null;
      var minArea = Infinity;

      function isInside(node, x, y) {
        if (!node.rect) {
          return false;
        }
        var lx = node.rect.x,
          ly = node.rect.y,
          rx = node.rect.width + lx,
          ry = node.rect.height + ly;
        return lx < x && x < rx && ly < y && y < ry;
      }
      if (self.nodes) {
        var activeNodes = self.nodes.filter(function(node) {
          if (!isInside(node, pos.x, pos.y)) {
            return false;
          }
          if (!node.rect) {
            return false;
          }
          // skip some types
          // console.log(node.type);
          if (["Layout", "Sprite"].includes(node.type)) {
            return false;
          }
          var area = node.rect.width * node.rect.height;
          if (area <= minArea) {
            minArea = area;
            self.nodeHovered = node;
          }
          return true;
        });
        activeNodes.forEach(function(node) {
          self.drawNode(node, "blue", true);
        });
        self.drawNode(self.nodeHovered, "blue");
      }
    },
    codeInsert: function(code) {
console.log(code);
    },
    codeRunDebugCode: function(code) {},
    activeMouseControl: function() {
      var self = this;
      var element = this.canvasfz;
      var mClicks = 0;
      var delay = 700;
      var timer = null;
      var screen = {
        bounds: {}
      };

      function calculateBounds() {
        var el = element;
        screen.bounds.w = el.offsetWidth;
        screen.bounds.h = el.offsetHeight;
        screen.bounds.x = 0;
        screen.bounds.y = 0;
        while (el.offsetParent) {
          screen.bounds.x += el.offsetLeft;
          screen.bounds.y += el.offsetTop;
          el = el.offsetParent;
        }
      }

      function activeFinger(index, x, y, pressure) {
        var scale = 0.5 + pressure;
        y = y - 50;
        self.fingerstyle =
          " display: block;border-color: #464646;border-width: 1mm;transform: translate3d(" +
          x +
          "px, " +
          y +
          "px, 0)";
        // self.$refs.finger
        //   .addClass("active")
        //   .css("transform", "translate3d(" + x + "px," + y + "px,0)");
      }

      function deactiveFinger(index) {
        self.fingerstyle = " ";
      }

      function mouseMoveListener(event) {
        var e = event;
        if (e.originalEvent) {
          e = e.originalEvent;
        }
        // Skip secondary click
        if (e.which === 3) {
          return;
        }
        // if (this.liveFlag) {
        //   this.clearCanvasRect();
        //   return;
        // }
        e.preventDefault();

        var pressure = 0.5;
        console.log(e.pageX, e.pageY);
        activeFinger(0, e.pageX, e.pageY, pressure);
        // that.touchMove(0, x / screen.bounds.w, y / screen.bounds.h, pressure);
      }

      function mouseDblClick(event) {
        self.doTouch(self.cursorValue.x, self.cursorValue.y);
      }

      function mouseUpListener(event) {
        var e = event;
        if (e.originalEvent) {
          e = e.originalEvent;
        }
        mClicks++;

        if (e.which === 3) {
          return;
        }
        e.preventDefault();
        var pos = coord(e);
        pos.px = Math.floor(pos.px * 1000) / 1000;
        pos.py = Math.floor(pos.py * 1000) / 1000;
        pos.x = Math.floor(pos.px * element.width);
        pos.y = Math.floor(pos.py * element.height);
        self.cursor = pos;
        markPosition(self.cursor);
        var distance =
          (pos.x - self.swipeStartPoint.x) * (pos.x - self.swipeStartPoint.x) +
          (pos.y - self.swipeStartPoint.y) * (pos.y - self.swipeStartPoint.y);

        if (mClicks === 1) {
          timer = setTimeout(function() {
            mClicks = 0;
          }, delay);

          if (distance > 10) {
            doSwipe(self.swipeStartPoint, self.cursor);
          } else if (!self.autoRec) {
            mouseDblClick(e);
            mClicks = 0;
          }
          console.log("click");
        } else {
          clearTimeout(timer);
          mouseDblClick(e);
          mClicks = 0;
          console.log("dblclick");
        }
        stopMousing();
      }

      function doSwipe(start, end) {
        var sx, sy, ex, ey;
        sx = start.px <= 0 ? 0.1 : start.px >= 1 ? 0.9 : start.px;
        sy = start.py <= 0 ? 0.1 : start.py >= 1 ? 0.9 : start.py;
        ex = end.px <= 0 ? 0.1 : end.px >= 1 ? 0.9 : end.px;
        ey = end.py <= 0 ? 0.1 : end.py >= 1 ? 0.9 : end.py;
        var code = "iqy.swipe(" + sx + "," + sy + "," + ex + "," + ey + ")";
        self.codeInsert(code);
        self.codeRunDebugCode(code);
      }

      function stopMousing() {
        element.removeEventListener("mousemove", mouseMoveListener);
        element.addEventListener("mousemove", mouseHoverListener);
        document.removeEventListener("mouseup", mouseUpListener);
        deactiveFinger(0);
      }

      function coord(event) {
        var e = event;
        if (e.originalEvent) {
          e = e.originalEvent;
        }
        calculateBounds();
        var x = e.pageX - screen.bounds.x;
        var y = e.pageY - screen.bounds.y;
        var px = x / screen.bounds.w;
        var py = y / screen.bounds.h;
        return {
          px: px,
          py: py,
          x: Math.floor(px * element.width),
          y: Math.floor(py * element.height)
        };
      }

      function mouseHoverListener(event) {
        var e = event;
        if (e.originalEvent) {
          e = e.originalEvent;
        }
        // Skip secondary click
        if (e.which === 3) {
          return;
        }
        e.preventDefault();
        // startMousing()

        if (!self.liveFlag) {
          var x = e.pageX - screen.bounds.x;
          var y = e.pageY - screen.bounds.y;

          var pos = coord(event);

          self.drawAllNode();
          if (self.nodeSelected) {
            self.drawNode(self.nodeSelected, "red");
          }
          self.drawHoverNode(pos);
          if (self.cursor.px) {
            markPosition(self.cursor);
          }
        }
      }

      function mouseDownListener(event) {
        var e = event;
        if (e.originalEvent) {
          e = e.originalEvent;
        }
        // Skip secondary click
        if (e.which === 3) {
          return;
        }
        e.preventDefault();

        var pos = coord(e);
        // change precision
        pos.px = Math.floor(pos.px * 1000) / 1000;
        pos.py = Math.floor(pos.py * 1000) / 1000;
        pos.x = Math.floor(pos.px * element.width);
        pos.y = Math.floor(pos.py * element.height);
        self.swipeStartPoint = pos;

        //fakePinch = e.altKey;
        calculateBounds();
        // startMousing()

        var x = e.pageX - screen.bounds.x;
        var y = e.pageY - screen.bounds.y;
        var pressure = 0.5;
        activeFinger(0, e.pageX, e.pageY, pressure);

        if (self.nodeHovered) {
          self.nodeSelected = self.nodeHovered;
          self.drawAllNode();
          // self.drawHoverNode(pos);
          self.drawNode(self.nodeSelected, "red");
          var generatedCode = self.generateNodeSelectorCode(self.nodeSelected);
          if (self.autoCopy) {
            copyToClipboard(generatedCode);
          }
          self.generatedCode = generatedCode;
          // self.editor.setValue(generatedCode);

          self.$jstree.jstree("deselect_all");
          self.$jstree.jstree("close_all");
          self.$jstree.jstree("select_node", "#" + self.nodeHovered.id);
          self.$jstree.jstree(true)._open_to("#" + self.nodeHovered.id);
          document.getElementById(self.nodeHovered.id).scrollIntoView(false);
        }
        // self.touchDown(0, x / screen.bounds.w, y / screen.bounds.h, pressure);

        element.removeEventListener("mousemove", mouseHoverListener);
        element.addEventListener("mousemove", mouseMoveListener);
        document.addEventListener("mouseup", mouseUpListener);
      }

      function markPosition(pos) {
        var ctx = self.canvasfz.getContext("2d");
        ctx.fillStyle = "#ff0000"; // red
        ctx.beginPath();
        ctx.arc(pos.x, pos.y, 12, 0, 2 * Math.PI);
        ctx.closePath();
        ctx.fill();

        ctx.fillStyle = "#fff"; // white
        ctx.beginPath();
        ctx.arc(pos.x, pos.y, 8, 0, 2 * Math.PI);
        ctx.closePath();
        ctx.fill();
      }

      /* bind listeners */
      element.addEventListener("mousedown", mouseDownListener);
      element.addEventListener("mousemove", mouseHoverListener);
    },
    websocketonopen() {
      //连接建立之后执行send方法发送数据
      // let actions = { test: "12345" };
      // this.websocketsend(JSON.stringify(actions));
      // console.log("open");
      this.websocketsend("on");
      console.log("open");
    },
    websocketonerror() {
      //连接建立失败重连
      this.initWebSocket();
    },
    drawCanvas(img) {
      const self = this;
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);

      var canvasRatio = this.canvas.width / this.canvas.height;
      if (canvasRatio > 1) {
        var minWidth = Math.min(self.leftWidth, this.canvas.width) - 50;

        this.scaledImageWidth = Math.floor(minWidth);
        this.scaledImageHeight = minWidth / canvasRatio;
      } else {
        var minHeight = Math.min(self.leftHeight, this.canvas.height) - 60;
        this.scaledImageWidth = minHeight * canvasRatio;
        this.scaledImageHeight = minHeight;
      }

      this.scaledImageWidth = Math.floor(this.scaledImageWidth);
      this.scaledImageHeight = Math.floor(this.scaledImageHeight);
      this.canvasfz.width = this.canvas.width = this.scaledImageWidth;
      this.canvasfz.height = this.canvas.height = this.scaledImageHeight;
      this.ctx.drawImage(
        img,
        0,
        0,
        img.width,
        img.height,
        0,
        0,
        this.scaledImageWidth,
        this.scaledImageHeight
      );
    },
    websocketonmessage(message) {
      //数据接收
const self = this;
var blob = new Blob([message.data], {type: 'image/png'})
var URL = window.URL || window.webkitURL;
var img = new Image();
img.onload = function() {
console.log(img.width, img.height);
self.canvasfz.width=self.canvas.width = img.width;
self.canvasfz.height=self.canvas.height = img.height;

self.gctx.drawImage(img, 0, 0);
img.onload = null;
var BLANK_IMG =
  'data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==';
img.src = BLANK_IMG;
img = null;
u = null;
blob = null;
}
var u = URL.createObjectURL(blob)
img.src = u

      // const redata = JSON.parse(e.data);
      // const self = this;
      // console.log("onmessage");
      // if (message.data instanceof Blob) {
      //   var blob = new Blob([message.data], {
      //     type: "image/jpeg"
      //   });

      //   // self.leftWidth=(self.screenWidth*self.splitterLeft/100)-10;

      //   var img = new Image();

      //   img.onload = function() {
      //     // console.log(img.width, img.height,self.leftWidth);
      //     self.canvas.height = img.height;
      //     self.canvas.width = img.width;
      //     // self.ctx.drawImage(img, 0, 0);
      //     self.drawCanvas(img);
      //   };
      //   img.src = URL.createObjectURL(blob);

      //   // self.wsimg=img;
      // }
    },
    websocketsend(Data) {
      //数据发送
      this.websock.send(Data);
    },
    websocketclose(e) {
      //关闭
      console.log("断开连接", e);
    },

    onResize(size) {
      this.report = size;
      // {
      //   width: 20 // width of container (in px)
      //   height: 50 // height of container (in px)
      // }
    },

    setRandomSize() {
      this.style = {
        width: Math.floor(100 + Math.random() * 200) + "px",
        height: Math.floor(100 + Math.random() * 200) + "px"
      };
    }
  },
    computed: {
          cursorValue: function () {
      if (this.showCursorPercent) {
        return {
          x: this.cursor.px,
          y: this.cursor.py
        }
      } else {
        return this.cursor
      }
    },
    leftStyle () {
      // 'height:100%;width:'+leftWidth+'px; padding:0px;overflow:hidden;'
      return {
        overflow:'hidden',
        padding:'0px',
        height:this.leftHeight+'px',
        width: this.getLeftWidth() + 'px'
      }
    }
  }
};
</script>
<style>
#left {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  flex: 1;
  min-width: 300px;
}
canvas{
    margin-top: 0px;
    margin-bottom: 0px;
    padding:0px;
    border:0px solid red;
}
#canvas {
  position: absolute;
  background: #d6f8ff;
  z-index: 0;

}
#canvasfz {
  position: absolute;
  background: rgba(255, 255, 255, 0);
  z-index: 1;
}
#footer {
  min-height: 100px;
  height: auto;
}
.finger {
  position: absolute;
  border-style: solid;
  border-radius: 50%;
  border-color: white;
  border-width: 0mm;
  width: 6mm;
  height: 6mm;
  top: -3mm;
  left: -3mm;
  opacity: 0.7;
  pointer-events: none;
  background: white;
  /*#464646;*/
  /*background: red;*/
  display: none;
}

.finger.active {
  display: block;
  border-color: #464646;
  border-width: 1mm;
}
</style>
