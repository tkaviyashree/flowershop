/*-------------------------------------------------------------------------------------------------------------------------------*/
/*This is main JS file that contains custom style rules used in this template*/
/*-------------------------------------------------------------------------------------------------------------------------------*/
/* Template Name: */
/* Version: 1.0 Initial Release*/
/* Build Date: 22-04-2015*/
/* Author: Unbranded*/
/* Website: 
/* Copyright: (C) 2015 */
/*-------------------------------------------------------------------------------------------------------------------------------*/

/*--------------------------------------------------------*/
/* TABLE OF CONTENTS: */
/*--------------------------------------------------------*/
/* 01 - VARIABLES */
/* 02 - page calculations */
/* 03 - function on document ready */
/* 04 - function on page load */
/* 05 - function on page resize */
/* 06 - swiper sliders */
/* 07 - buttons, clicks, hovers */
/* 08 - function on page scroll */
/*-------------------------------------------------------------------------------------------------------------------------------*/

/*================*/
/* 01 - VARIABLES */
/*================*/
var swipers = [], winW, winH, winScr, _isresponsive, smPoint = 768, mdPoint = 992, lgPoint = 1200, addPoint = 1600, _ismobile = navigator.userAgent.match(/Android/i) || navigator.userAgent.match(/webOS/i) || navigator.userAgent.match(/iPhone/i) || navigator.userAgent.match(/iPad/i) || navigator.userAgent.match(/iPod/i);


$(function() {

	"use strict";

	/*========================*/
	/* 02 - page calculations */
	/*========================*/
	function pageCalculations(){
		winW = $(window).width();
		winH = $(window).height();
		if($('.menu-button').is(':visible')) _isresponsive = true;
		else _isresponsive = false;
	}

	/*=================================*/
	/* 03 - function on document ready */
	/*=================================*/
	pageCalculations();

	/*============================*/
	/* 04 - function on page load */
	/*============================*/
	$(window).load(function(){
		$('#loader-wrapper').fadeOut();
		initSwiper();
	});

	/*==============================*/
	/* 05 - function on page scroll */
	/*==============================*/
	$(window).scroll(function(){
		winScr = $(window).scrollTop();
		if(winScr>=145){$('header:not(.type-3)').addClass('move');}
		else {$('header:not(.type-3)').removeClass('move');}

		if(winScr>=115){$('header.type-3').addClass('move');}
		else {$('header.type-3').removeClass('move');}		
	});

	/*==============================*/
	/* 05 - function on page resize */
	/*==============================*/
	function resizeCall(){
		pageCalculations();

		$('.swiper-container.initialized[data-slides-per-view="responsive"]').each(function(){
			var thisSwiper = swipers['swiper-'+$(this).attr('id')], $t = $(this), slidesPerViewVar = updateSlidesPerView($t), centerVar = thisSwiper.params.centeredSlides;
			thisSwiper.params.slidesPerView = slidesPerViewVar;
			thisSwiper.reInit();
			if(!centerVar){
				var paginationSpan = $t.find('.pagination span');
				var paginationSlice = paginationSpan.hide().slice(0,(paginationSpan.length+1-slidesPerViewVar));
				if(paginationSlice.length<=1 || slidesPerViewVar>=$t.find('.swiper-slide').length) $t.addClass('pagination-hidden');
				else $t.removeClass('pagination-hidden');
				paginationSlice.show();
			}
		});
	}
	if(!_ismobile){
		$(window).resize(function(){
			resizeCall();
		});
	} else{
		window.addEventListener("orientationchange", function() {
			resizeCall();
		}, false);
	}

	/*=====================*/
	/* 06 - swiper sliders */
	/*=====================*/
	function initSwiper(){
		var initIterator = 0;
		$('.swiper-container').each(function(){								  
			var $t = $(this);								  

			var index = 'swiper-unique-id-'+initIterator;

			$t.addClass('swiper-'+index + ' initialized').attr('id', index);
			$t.find('.pagination').addClass('pagination-'+index);

			var autoPlayVar = parseInt(($t.attr('data-autoplay')), 10);
			var centerVar = parseInt(($t.attr('data-center')), 10);
			var simVar = ($t.closest('.circle-description-slide-box').length)?false:true;

			var slidesPerViewVar = $t.attr('data-slides-per-view');
			if(slidesPerViewVar == 'responsive'){
				slidesPerViewVar = updateSlidesPerView($t);
			}
			else if(slidesPerViewVar != 'auto') slidesPerViewVar = parseInt(slidesPerViewVar, 10);

			var loopVar = parseInt(($t.attr('data-loop')), 10);
			var speedVar = parseInt(($t.attr('data-speed')), 10);
			var modeVar = $t.attr('data-mode');

			swipers['swiper-'+index] = new Swiper('.swiper-'+index,{
				speed: speedVar,
				pagination: '.pagination-'+index,
				loop: loopVar,
				paginationClickable: true,
				autoplay: autoPlayVar,
				slidesPerView: slidesPerViewVar,
				keyboardControl: true,
				calculateHeight: true, 
				simulateTouch: simVar,
				centeredSlides: centerVar,
				roundLengths: true,
				mode: modeVar,

				onSlideChangeEnd: function(swiper){
					var activeIndex = (loopVar===1)?swiper.activeLoopIndex:swiper.activeIndex;
					var qVal = $t.find('.swiper-slide-active').attr('data-val');
					$t.find('.swiper-slide[data-val="'+qVal+'"]').addClass('active');
				},
				onSlideChangeStart: function(swiper){
					var activeIndex = (loopVar===1)?swiper.activeLoopIndex:swiper.activeIndex;
					$t.find('.swiper-slide.active').removeClass('active');
					if($t.parent().hasClass('swiper-chained-top')) {
						swipers['swiper-'+$t.parent().next().find('.swiper-container').attr('id')].swipeTo(activeIndex);
						$t.parent().next().find('.swiper-slide.chained-active').removeClass('chained-active');
						$t.parent().next().find('.swiper-slide').eq(activeIndex).addClass('chained-active');
						swipers['swiper-'+$t.parent().next().find('.swiper-container').attr('id')].swipeTo(activeIndex);
					}
				},
				onSlideClick: function(swiper){
					if($t.parent().hasClass('swiper-chained-bottom')) swipers['swiper-'+$t.parent().prev().find('.swiper-container').attr('id')].swipeTo(swiper.clickedSlideIndex);
				}
			});
			swipers['swiper-'+index].reInit();
			if(!centerVar){
				if($t.attr('data-slides-per-view')=='responsive'){
					var paginationSpan = $t.find('.pagination span');
					var paginationSlice = paginationSpan.hide().slice(0,(paginationSpan.length+1-slidesPerViewVar));
					if(paginationSlice.length<=1 || slidesPerViewVar>=$t.find('.swiper-slide').length) $t.addClass('pagination-hidden');
					else $t.removeClass('pagination-hidden');
					paginationSlice.show();
				}
			}
			initIterator++;
		});

	}

	function updateSlidesPerView(swiperContainer){
		if(winW>=addPoint) return parseInt(swiperContainer.attr('data-add-slides'), 10);
		else if(winW>=lgPoint) return parseInt(swiperContainer.attr('data-lg-slides'), 10);
		else if(winW>=mdPoint) return parseInt(swiperContainer.attr('data-md-slides'), 10);
		else if(winW>=smPoint) return parseInt(swiperContainer.attr('data-sm-slides'), 10);
		else return parseInt(swiperContainer.attr('data-xs-slides'), 10);
	}

	//swiper arrows
	$('.swiper-arrow-left').on('click', function(){
		swipers['swiper-'+$(this).parent().find('.swiper-container').attr('id')].swipePrev();
	});

	$('.swiper-arrow-right').on('click', function(){
		swipers['swiper-'+$(this).parent().find('.swiper-container').attr('id')].swipeNext();
	});

	//swiper tabs
	$('.swiper-one').on('click', function(){
		var index = $(this).parent().parent().find('.swiper-tab').index($(this).parent());
		$(this).parent().find('.active').removeClass('active');
		swipers['swiper-'+$(this).closest('.swiper-img').prev().find('.swiper-container').attr('id')].swipeTo(index);
		return false;
	});
	/*==============================*/
	/* 07 - buttons, clicks, hovers */
	/*==============================*/

	//responsive menu
	$('.menu-icon').on("click",function(){
		$('header').toggleClass("active");
		return false;
	});

	$('.sub-menu a .fa').on('click', function(){
		$(this).parent().next().slideToggle();
		$(this).toggleClass("active");
		return false;
	});
	$('.sub-menu a .fa').on('click', function(){
		$(this).parent().toggleClass("active");
		return false;
	});

	//tabs drop-down
	$('.tabs-drop').on('click', function(){
		$(this).parent().toggleClass('active');
	});

	// search dropdown
	$('.icon-search').on('click', function(){
		$(this).parent().toggleClass('active');
	});


	// 
	$(".sort .text-sort span").on("click",function(){
    	$(this).next().slideToggle('active');
    	return false;
    })

	//accordeon
	$('.accordeon-title').on('click', function(){
		$(this).toggleClass('active');
		$(this).next().slideToggle();
	});

	//product detail preview
	$('.small-ph a').on('click', function(){
		if($(this).hasClass('active')) return false;
		$(this).parent().find('a').removeClass('active');
		$(this).addClass('active');
		$('.preview-image').attr('src', $(this).data('src')).attr('data-preview', $(this).data('preview'));
		return false;
	});

	$('.preview-zoom-image').on('click', function(){
		$('.image-preview-popup .cell-view img').attr('src', $('.small-ph a.active').data('preview'));
		$('.image-preview-popup').addClass('active');
		return false;
	});

	$('.image-preview-popup .close-popup').on('click', function(){
		$('.image-preview-popup').removeClass('active');
		return false;
	});
	
	//tabs
	var tabFinish = 0;
	$('.tab-switch').on('click', function(){
		if($(this).hasClass('active') || tabFinish == 1) return false;
		tabFinish = 1;
		var thisParent = $(this).closest('.tabs'), thisIndex = $(this).parent().find('.tab-switch').index(this);
		thisParent.find('.tab-switch.active').removeClass('active');
		$(this).addClass('active');
		thisParent.find('.tabs-drop').text($(this).text()).click();
		thisParent.find('.tab-wrapper:visible').fadeOut(
			function(){thisParent.find('.tab-wrapper').eq(thisIndex).fadeIn(
				function(){tabFinish = 0;});
		});

	});

    //Tabs
	var tabSelectFinish = 0;
	$('.tt-nav-tab-item').on('click', function(){		
	    var $t = $(this);
	    if(tabSelectFinish || $t.hasClass('active')) return false;
	    tabSelectFinish = 1;
	    $t.closest('.tt-nav-tab').find('.tt-nav-tab-item').removeClass('active');
	    $t.addClass('active');
	    var index = $t.parent().parent().find('.tt-nav-tab-item').index(this);
	    $t.parents('.tt-tab-nav-wrapper').find('.tt-tab-select select option:eq('+index+')').prop('selected', true);
	    $t.closest('.tt-tab-wrapper').find('.tt-tab-info:visible').fadeOut(500, function(){
	    	var $tabActive  = $t.closest('.tt-tab-wrapper').find('.tt-tab-info').eq(index);
	    	$tabActive.css('display','block').css('opacity','0');
	    	$tabActive.animate({opacity:1});
	    	 tabSelectFinish = 0;
	    });
	});
	$('.tt-tab-select select').on('change', function(){
	    var $t = $(this);
	    if(tabSelectFinish) return false;
	    tabSelectFinish = 1;    
	    var index = $t.find('option').index($(this).find('option:selected'));
	    $t.closest('.tt-tab-nav-wrapper').find('.tt-nav-tab-item').removeClass('active');
	    $t.closest('.tt-tab-nav-wrapper').find('.tt-nav-tab-item:eq('+index+')').addClass('active');
	    $t.closest('.tt-tab-wrapper').find('.tt-tab-info:visible').fadeOut(500, function(){
	    	var $tabActive  = $t.closest('.tt-tab-wrapper').find('.tt-tab-info').eq(index);
	    	$tabActive.css('display','block').css('opacity','0');
	    	$tabActive.animate({opacity:1});
	    	 tabSelectFinish = 0;
	    });
	});		

	//counters
	$('.tt-counter').viewportChecker({
		classToAdd: 'counted',
		offset: 100,
		callbackFunction: function(elem, action){
			elem.find('.tt-counter-number').countTo();		
		}		
	});

	//video
	$('.tt-video-play').on("click", function(){
		var video = $(this).attr('href');			
		$(this).siblings('.tt-video-iframe').show().find('iframe').attr('src',video);
		return false;
	});
	$('.tt-video-close').on("click", function(){
		$(this).parent().hide();		
		$(this).siblings('iframe').attr('src','about:blank');
		return false;
	});

	//progress bar
	$('.tt-progress-block').viewportChecker({
		offset: 100,
		callbackFunction: function(elem, action){
			elem.find('.count').countTo();
			
			var $progress_bar = elem.find('.tt-progress-bar'),
				speed = parseInt($progress_bar.attr("data-speed"),10),
				to = parseInt($progress_bar.attr("data-to"),10);
			$progress_bar.animate({width: to+"%"}, {duration: speed});		
		}		
	});			

});