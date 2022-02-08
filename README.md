# Web-Scraping-Javascript
Web Scraping through Javascript

cats = [
    "https://www.Insert Webiste"
];

steps.start = function(){
    //setSettings({skipVisited:true});
    //clearCookies();
	cats.forEach(function(v){
		next(v,"category");
	});
	done();
};

steps.category = function(){
	if($("a.product-card__buy-btn.product_card_btn_text_class").length>0){
        $("a.product-card__buy-btn.product_card_btn_text_class").each(function(i,v) {
            next(v.href, "products");
         });    
    }
    done(1000);
};

steps.products = function() {
	wait(".page-product .page-header h1",5000).always(function(){
	    var item = {};
    	item.Retailer = "Insert Retailer Name";
		item.Variant_Name = $(".pdp__title").text().trim();
    	item.Price = $("span.product-modal-form__total").text().trim();
    	item.Category = $(".product-card__tag-text.pdp_product_type").text().trim();
        item.Flavour = $(".col-sm-6.col-md-6 p").text().trim();
        emit("Name", [item]);
    	done();
	});
};

