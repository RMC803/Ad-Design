# Ad-Design
//Random text movement 


background(38, 0, 255);
fill(196, 255, 0);

draw = function() {
     textSize(30);
     var myName = "Decadence";
     text(myName, 80, 100);
     textSize(40);
     text(myName, 50, 200);
     textSize(50);
     text(myName, 60, 300);
};

$(document).ready(function() {
    animateDiv($('.a'));
        animateDiv($('.b'));
        animateDiv($('.c'));

});

function makeNewPosition($container) {

    // Get viewport dimensions (remove the dimension of the div)
    var h = $container.height() - 50;
    var w = $container.width() - 50;

    var nh = Math.floor(Math.random() * h);
    var nw = Math.floor(Math.random() * w);

    return [nh, nw];

}

function animateDiv($target) {
    var newq = makeNewPosition($target.parent());
    var oldq = $target.offset();
    var speed = calcSpeed([oldq.top, oldq.left], newq);

    $target.animate({
        top: newq[0],
        left: newq[1]
    }, speed, function() {
        animateDiv($target);
    });

};

function calcSpeed(prev, next) {

    var x = Math.abs(prev[1] - next[1]);
    var y = Math.abs(prev[0] - next[0]);

    var greatest = x > y ? x : y;

    var speedModifier = 0.1;

    var speed = Math.ceil(greatest / speedModifier);

    return speed;

}
