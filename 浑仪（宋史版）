module ring(d,rot=[0,0,0]){
  rotate(rot)rotate_extrude(){
    translate([d,0,0])children();
  }
}

module ring_rail(d,sec=[1,1,1/3],rot=[0,0,0]){
  ring(d,rot){
    translate([0,sec[1]/3,0])square([sec[0],sec[1]/3],center=true);
    translate([0,-sec[1]/3,0])square([sec[0],sec[1]/3],center=true);
    translate([sec[0]/2-sec[2]/2,0,0])square([sec[2],sec[1]],center=true);
  }
}

$fn=360;
unit = 31.68/24;

//translate([0,0,-100])cube([230,230,1],center=true);
// day=0,alpha=0,beta=0,
// latitude=42,size=61.3*unit,thick=1.2*unit,cursor=2

module hunyi_rules(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  一曰双规皆径六尺一寸三分围一丈八尺三寸九分广四寸五分
  //  上刻周天三百六十五度南北并立置水臬以为准得出地三十五
  //  度乃北极出地之度也以釭贯之四面皆七十二度属紫微宫星凡
  //  三十七坐一百七十有五星四时常见谓之上规中一百一十度四
  //  面二百二十度属黄赤道内外官星二百四十六坐一千二百八十
  //  九星近日而隐远而见谓之中规置臬之下绕南极七十二度除老
  //  人星外四时常隐谓之下规
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  d=refRing;
  w=refThickness;

  // 子午圆
  ring_rail(d/2,[w*2,w*2,0],[0,90,0]);
  // 赤道定圆
  rotate([latitude,0,0]){
    ring_rail(d/2,[w*2,w,w*2],[0,0,0]);
  }
}

module hunyi_cursor(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  二曰游规径五尺二寸围一丈五尺六寸广一寸二分厚四分上亦刻周天以
  //  釭贯于双规巅轴之上令得左右运转凡置管测验之法众星远近随天周遍
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  d=refRing/61.3*52;
  w=refThickness;
  t=refThickness/1.2*0.4;
  rotate([latitude,0,0])rotate([0,0,day*360/365.25]){
    // 二分环
    color("pink")ring_rail(d/2,[w,t,w],[0,90,0]);
    // 二至环
    color("pink")ring_rail(d/2,[w,w,0],[90,0,0]);
    translate([0,0,d/2+w])cylinder(d=w*2/3,h=w*6,center=true);
    translate([0,0,-d/2-w])cylinder(d=w*2/3,h=w*6,center=true);
  }
}

module hunyi_straight(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  三曰直规二各长四尺八寸阔一寸二分厚四分于两极之间用夹窥管中置
  //  关轴令其游规运转
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  d=refRing/61.3*48;
  w=refThickness;
  t=refThickness/1.2*0.4;

  rotate([latitude,0,0])rotate([0,0,day*360/365.25])rotate([0,0,alpha]){
    // 悬枢
    ring_rail(d/2,[w,w,0],[0,90,0]);
    rotate([0,0,0])union(){
      translate([w/2-(w-t)/4,0,0])cube([t,w,d],center=true);
      translate([-w/2+(w-t)/4,0,0])cube([t,w,d],center=true);
    }
  }
}

module hunyi_aim(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  四曰窥管一长四尺八寸广一寸二分关轴在直规中
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  d=refRing/61.3*48;
  w=refThickness;
  t=refThickness/1.2*0.4;

  rotate([latitude,0,0])rotate([0,0,day*360/365.25])rotate([0,0,alpha]){
    // 窥管
    rotate([beta,0,0])difference(){
      union(){
        color("black")cylinder(h=d,d=t,center=true);
        rotate([0,90,0])cylinder(h=w,d=w,center=true);
      }
      color("black")cylinder(h=d+1,d=t/2,center=true);
    }
  }
}

module hunyi_horizontal(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  五曰平准轮在水臬之上径六尺一寸三分围一丈八尺三寸九分上刻八卦
  //  十干十二辰二十四气七十二候于其中，定四维日辰，正昼夜百刻
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  d=refRing;
  w=refThickness;
  
  ring_rail(d/2,[w*2,w*2,w*2],[0,0,0]);
    for(i=[0:360/24:360]){
      rotate([0,0,i])translate([d/2,0,0])difference(){
        translate([0,0,0])cube([w*2.1,w,w*2],center=true);
        //rotate([0,90,0])cylinder(d=thick/3,h=dEarth+2,center=true);
        //translate([-thick/2,0,thick])cube([thick,gap,gap],center=true);
      }
    }
}

module hunyi_ecliptic(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  六曰黄道南北各去赤道二十四度东西交于卯酉以为日行盈缩月行九道
  //  之限凡冬至日行南极去北极一百一十五度故景长而寒夏至日在赤道北
  //  二十四度去北极六十七度故景短而暑月有九道之行岁匝十二辰正交出
  //  入黄道远不过六度五星顺留伏逆行度之常数也
  ////

  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  w=refThickness;
  t=refThickness/1.2*0.4;
  d=refRing/61.3*52;
  
        
  // 黄道   夹角（23.26）y轴
  rotate([latitude,0,0])rotate([0,0,day*360/365.25])rotate([0,23+26/60,0]){
    color("yellow"){
      ring_rail(d/2,[w,w,0],[0,0,0]);
      for(i=[0:30:360]){
        rotate([0,0,i])translate([d/2,0,0])difference(){
          translate([0,0,0])cube([w,w,w],center=true);
          rotate([0,90,0])cylinder(d=t/3,h=t+1,center=true);
        }
      }
    }
  }
}

module hunyi_equator(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  七曰赤道与黄道等带天之纮以隔黄道去两极各九十一度强黄道之交也
  //  按经东交角宿五度少西交奎宿一十四度强日出于赤道外远不过二十四
  //  度冬至之日行斗宿日入于赤道内亦不过二十四度夏至之日行井宿及昼
  //  夜分炎凉等日月五星阴阳进退盈缩之常数也
  ////
  
  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  w=refThickness;
  t=refThickness/1.2*0.4;
  d=refRing/61.3*52;

          
  // 赤道
  rotate([latitude,0,0])rotate([0,0,day*360/365.25])color("red"){
    ring_rail(d/2,[w,t,w],[0,0,0]);
    // 始于女
    //for(i=[280, -67.5, -52.5, -37.5, -22.5, -10, 0, 10, 22.5, 37.5, 52.5, 67.5, 80, 90, 100, 112.5, 127.5, 142.5, 157.5, 170, 180, 190, 202.5, 217.5, 232.5, 247.5, 260, 270]){
    for(i=[11.8356164383562,20.7123287671233,35.5068493150685,40.4383561643836,45.3698630136986,63.1232876712329,73.972602739726,99.8630136986301,107.753424657534,119.58904109589,129.452054794521,146.219178082192,162,170.876712328767,186.657534246575,198.493150684932,212.301369863014,223.150684931507,238.931506849315,240.904109589041,249.780821917808,282.328767123288,286.27397260274,301.068493150685,307.972602739726,325.72602739726,343.479452054795,360.246575342466]){
      rotate([0,0,i-11.8356164383562])translate([d/2,0,0])difference(){
        translate([0,0,0])cube([w,w,t],center=true);
        //rotate([0,90,0])cylinder(d=thick/3,h=thick+2,center=true);
      }
    }
  }
}

module hunyi_pillar(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  八曰龙柱四各高五尺五寸并于平准轮下
  ////
  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  a=refRing/2;
  a1=refRing/61.3*75;
  h=refRing/61.3*55;
  d=refThickness/1.2*3.5;

  rotate([0,0,45]){
    //hull(){
    //  translate([0,0,-a])sphere(d=d/2,$fn=60);
    //  translate([0,0,-h])sphere(d=d,$fn=60);
    //}
    for(i=[[-1,0],[1,0],[0,-1],[0,1]]){
      hull(){
        translate([i[0]*a,i[1]*a,0])sphere(d=d/2,$fn=60);
        translate([i[0]*(a1*0.707-d),i[1]*(a1*0.707-d),-h])sphere(d=d/2,$fn=60);
      }
      //translate([i[0]*(a1*0.70-d),i[1]*(a1*0.70-d),-h/2])cylinder(d1=d,d2=d/2,h=h,center=true);
    }
  }
}

module hunyi_base(paraActive=[0,0,0],paraStatic=[35/365.25*360,61.3,1.2]){
  ////
  //  九曰水臬十字为之其水平满北辰正以置四隅各长七尺五寸高三寸半深
  //  一寸四隅水平则天地准
  ////
  
  day   = paraActive[0];
  alpha = paraActive[1];
  beta  = paraActive[2];
  latitude     = paraStatic[0];
  refRing      = paraStatic[1];
  refThickness = paraStatic[2];

  a=refRing;
  a1=refRing/61.3*75;
  h1=refRing/61.3*55;
  h=refRing/61.3*3.5;
  b=refRing/61.3*1;
  d=refThickness/1.2*3.5;

  rotate([0,0,0])difference(){
    union(){
      for(i=[-1:2:1]){
        translate([i*(a1/2-d/2),0,-h1-h/2])cube([h,a1,h],center=true);
        translate([0,i*(a1/2-d/2),-h1-h/2])cube([a1,h,h],center=true);
      }
      translate([0,0,-h1-h/2])cube([h,a1,h],center=true);
      translate([0,0,-h1-h/2])cube([a1,h,h],center=true);
    }
    rotate([0,0,0])translate([0,0,-h1])rotate([0,0,0])cube([a,b*1.5,b*1.5],center=true);
    rotate([0,0,90])translate([0,0,-h1])rotate([0,0,0])cube([a,b*1.5,b*1.5],center=true);
  }
}

module hunyi(day=0,alpha=0,beta=0,latitude=42,refRing=61.3*unit,refThickness=1.2*unit){
  paraActive=[day,alpha,beta];
  paraStatic=[90-latitude, refRing, refThickness];

  hunyi_rules(paraActive,paraStatic);
  hunyi_cursor(paraActive,paraStatic);
  hunyi_straight(paraActive,paraStatic);
  hunyi_aim(paraActive,paraStatic);
  hunyi_horizontal(paraActive,paraStatic);
  hunyi_ecliptic(paraActive,paraStatic);
  hunyi_equator(paraActive,paraStatic);
  hunyi_pillar(paraActive,paraStatic);
  hunyi_base(paraActive,paraStatic);
}

hunyi($t*365*2,-$t*360/2,-$t*360*4);
//hunyi($t*365*2,-$t*360/2,-$t*360*4,35,refRing=100,refThickness=3);
