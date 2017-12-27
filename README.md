//*module for init slider on the home page*//

var headerScroll = (($) => {

    'use strict';

    var didScroll;
    var lastScrollTop = 0;
    var DELTA = 1;
    const SCROLL_HEIGHT = 1;

    function init() {

        if (!$('.header').length) {
            return;
        }
        $(window).scroll(function(event) {
            didScroll = true;
        });

        setInterval(function() {
            if (didScroll) {
                hasScrolled();
                didScroll = false;
            }
        }, 250);

    }

    function hasScrolled() {
        var st = $(window).scrollTop();
        if (st > 100) {
            if (Math.abs(lastScrollTop - st) <= DELTA)
                return;
            if (st > lastScrollTop && st > SCROLL_HEIGHT) {
                $('.header').removeClass('nav-down').addClass('nav-up');
            } else {
                if (st + $(window).height() < $(document).height()) {
                    $('.header').removeClass('nav-up').addClass('nav-down');
                }
            }

            lastScrollTop = st;
        } else {
            $('.header').removeClass('nav-up').addClass('nav-down');
        }

    }
    return {

        init: init

    };
})(jQuery);

export default headerScroll;
