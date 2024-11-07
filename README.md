# Add mask for date field along with validator
- Validator and Mask Date in JavaScript
- Simultaneous use of mask and date validation for date fields
Support Farsi, Arabic and English keyboards
- You can also customize the second input of the function according to the usage

# requirement
  jquery
  jquery.inputmask.bundle

# Usage/Examples



function validDate (input, format = "YYYY/mm/dd") {

	var
	regex = "^",
	regexformat = {
		"YYYY"  : "[۱1١][۲۳۴۵۶۷۸۹23456789٢٣٤٥٦٧٨٩][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]{2}",
		"mm"    : "([۰0٠][۱۲۳۴۵۶۷۸1-9١٢٣٤٥٦٧٨٩]|[۱1١][۰۱۲0-2٠١٢])",
		"mm/dd" : "([۰0٠][۱۲۳۴۵۶1-6١٢٣٤٥٦]\/([۰0٠][۱۲۳۴۵۶۷۸۹1-9١٢٣٤٥٦٧٨٩]|[۱۲12١٢][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]|[۳3٣][۰0٠۱1١])|[۰0٠][۷۸۹7-9٧٨٩]\/([۰0٠][۱۲۳۴۵۶۷۸۹1-9١٢٣٤٥٦٧٨٩]|[۱۲12١٢][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]|[۳3٣][۰0٠])|[۱1١][۰۱۲0-2٠١٢]\/([۰0٠][۱۲۳۴۵۶۷۸۹1-9١٢٣٤٥٦٧٨٩]|[۱۲12١٢][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]|[۳3٣][۰0٠]))",
		"dd"    : "([۰۱01٠١][۰۱۲۳۴۵۶۷۸۹\d٠١٢٣٤٥٦٧٨٩]|[۲2٢][۰۱۲۳۴01234٠١٢٣٤]|[۳3٣][۰۱01٠١])",
		"H"     : "([۰۱01٠١][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]{1}|[۲2٢][۰۱۲۳۴01234٠١٢٣٤])",
		"i"     : "([۰۱۲۳۴۵012345٠١٢٣٤٥][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]{1})",
		"s"     : "([۰۱۲۳۴۵012345٠١٢٣٤٥][۰۱۲۳۴۵۶۷۸۹\\d٠١٢٣٤٥٦٧٨٩]{1})",
	};
	regex += format.replace(/mm\/dd|[^\/|\s|\:]+/gm, function(a, b){
		if (regexformat[a] != undefined)
			return regexformat[a];
		else
			return "";
	});
	regex += "$";
	$(input).inputmask({
		regex: regex,
		clearIncomplete: true,
		isComplete: function(buffer, opts) {
			let 
			date   = buffer.join(''),
			result = new RegExp(opts.regex).test(buffer.join(''));
			if (format.indexOf("YYYY/mm/dd") === 0) {
				if (date.length > 0) {
					date 	= date.split('/');
					var daydate = date[2].split(' ');
					if (date[1] == '12' && daydate[0] == '30')
						return ((Number(date[0]) - (Number(date[0]) > 0 ? 474 : 473)) % 2820 + 474 + 38) * 682 % 2816 < 682;
				}
			}
			return result;
		}
	});
}
