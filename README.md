# Legislative-Bill-Text-Extraction
This python script downloads North Carolina General Assembly bills as pdfs and extracts text for analysis. The goal is to quickly summarize information about the bills a particular legislator sponsored, such as which other legislators he or she cosponsors bills with and the topics they most often pursue policy on. This python script performs a search on the North Carolina Legislature's bill search website. The user provies keyword(s) to search on, such as a legislator's name, as well as the legislative session to search on (e.g., 2019-2020 session).

## Usage
First, we use the selenium package to navigate to the search site: https://www.ncleg.gov/Search/BillText. This form accepts a number of inputs, including key terms to search on as well as the session to filter by. Selenium navigates to these input boxes and dropdowns using xpaths to target the elements. Having filled these inputs, it clicks the Search button.

![bill_search](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/bill_search.png?raw=true)

Selenium sends keys to the form.

![bill_search_filled_in](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/bill_search_filled_in.png?raw=true)

The retrieveBills() function loops through each bill.

![retrieveBills1](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/retrieveBills1.png?raw=true)

We use xpaths to access elements of the webpage.

![retrieveBills2](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/retrieveBills2.png?raw=true)

The results page gives us a list of bills that match the criteria we provided. Our code walks in and out of each bill's page, retrieving firstly the information (metadata) about the bill, such as bill number, bill name, and who sponsored it.

![bill_search_results](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/bill_search_results.png?raw=true)

Then it reads and downloads the PDF of the latest version of the bill, in official language. The raw text of the bill is later used for textual analysis.

![retrieveBills3](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/retrieveBills3.png?raw=true)

We retrieve a handful of elements from the description page: bill number, bill name, sponsors, and keywords.

![bill_description_example](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/bill_description_example.png?raw=true)

Then we click into the bill itself.

![text_extractor](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/text_extractor.png?raw=true)

We download the pdf to a directory designated by the user (must update selenium driver options to allow direct lownloads). Then extract the raw text from the pdf document.

![bill_text_example](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/bill_text_example.png?raw=true)

Our code extracts text on a page-by-page basis and stores each as an element in a dict. It then concatenates all pages of a bill together for a single text object.

![page_compiler](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/page_compiler.png?raw=true)

The pdfExtractor() method leverages the text_extractor() and page_compiler() sub-methods.

![pdfExtractor](https://github.com/drussel4/Text-Extraction/blob/master/img/HowToUse/pdfExtractor.png?raw=true)

The retrieval portion of the code is complete! Now we want to see what we've got.

Having retrieved metadata and raw text for each bill, we generate three exhibits:
1. A wordcloud that showcases the frequency of terms in the raw text of every bill that was returned in the search results.

![wordcloud_exhibit](https://github.com/drussel4/Text-Extraction/blob/master/img/Exhibits/wc_exhibit.png?raw=true)

2. A bar chart displaying the frequency of sponsors on the bills returned in the search results. In this way we can see the legislators that collaborate most frequently with the legislator we searched on.

![sponsors_exhibit](https://github.com/drussel4/Text-Extraction/blob/master/img/Exhibits/sponsors_exhibit.png?raw=true)

3. A bar chart displaying the frequency of key terms associated with the bills returned in the search results. In this way we can see the pursued by the legislator we searched on.

![keywords_exhibit](https://github.com/drussel4/Text-Extraction/blob/master/img/Exhibits/keywords_exhibit.png?raw=true)

## License

MIT © Dave Russell
