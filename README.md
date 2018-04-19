# Planet Netsweeper

This repository contains supporting data for the [Citizen Lab report about global Netsweeper installations](  https://citizenlab.ca/2018/04/planet-netsweeper/).

CSVs are provided as summaries of the most relevant data points while raw data is also included for those who
wish to look at a more detailed information.

This release includes a PostgreSQL 9.4 database dump of raw data that was collected from August 31, 2017 to April 9, 2018.
This file is ```raw_data_collected.sqlc``` and can be restored from the custom PostgreSQL format using pg_restore tool.

# CSV Summaries

This folder contains summaries of data extracted from the full data collection.  It also contains any data annotations
and notes that were added to data after collection.

The following summaries are contained:

* **blocks_found.csv** - All URLs that were found to return what appears to be Netsweeper formatted iframes.
* **host_header_results.csv** - All IP ranges that returned what appeared to be Netsweeper formatted iframes to our requests.
* **host_header_bahrain.csv** - All URLs that returned www.anonymous.com.bh injections based on testing the [Bahrain local list](https://github.com/citizenlab/test-lists/blob/master/lists/bh.csv).
* **installations_found_ALL.csv** - All IPs that returned any positive result for our scans for Netsweeper installations.
* **installations_found_SUBSET.csv** - Same as above but only the subset of country cases where human rights concerns may be present.
* **uae-incountry-testing.csv** - Results of in-country testing done on du in UAE on April 9th, 2018.
* **ye-incountry-testing.csv** -  Results of in-country testing done Yemen during August, 2017.

# Schemas explained

## blocks_found.csv

* cc - Country code.
* url - URL that was being tested.
* comment - Any annotation about geoip or asn corrections.
* first_seen - First datetime the block was seen within the test period.
* last_seen - Last datetime the block was seen within the test period.
* blocked_ct - How many times the block was seen.
* blocked_by_ip_ct - How many unique IPs are referenced in the injected iframe.
* cat_ct - How many categories was this URL seen categorized as.
* most_seen_cat - The most commonly seen category this URL was categorized as.
* sample_iframe - A sample of an injected iframe for the country/URL combination. 
* sample_ref - A sample measurement URL where a positive case is seen.

## host_header_results.csv

* suspected_cat - The category we expect our host header would match against.
* ip_range - The /24 prefix where we get the injection from.
* count - The number of unique IPs that returned injections within the /24 prefix.
* country - Country code.
* asn_name - ASN name.
* asn_num - ASN number.
* sample_banner - A sample banner that was returned from the IP.

## host_header_bahrain.csv

* url - The URL that was tested.
* injection_count - The number of injections that were returned in the TCP stream (out of a total of three)

## installations_found_ALL.csv and installations_found_SUBSET.csv

* country - Country code.
* as_name - ASN name that the installation belongs to.
* ip - IP address that matched our signature at any point in time.
* comment - Any annotation/comment that was added.
* as_num - ASN Number.
* first_seen - First time we see the IP in our data collection period.
* last_seen- Last time we see the IP in our data collection period.
* b_date - The datetime where we see the most positive cases of the behaviours we look for on this IP
* ooni - Boolean if we see this IP in measurement data (ooni or iclab)
* b1,b2,b3,b4,b5,b6 - Boolean of the test code on the behaviours we look for (see table for equivalencies).  We return the most seen positives during testing period.
* b_snmp - Does the SNMP sysdescr value contain ".netsw"
* snmp_sysdescr - Most recent non-blank SNMP sysdescr value.
* snmp_date - Date when this SNMP value was returned.
* rdns - Most recent non-blank reverse dns value.
* rdns_date - Date when the rdns value was returned.
* denypage_title - Most recent non blank deny page title.
* denypage_title_date - Date the deny page title value was collected.
* denypage_mailto - Most recent non blank deny page mailto.
* denypage_mailto_date - Date the deny page mailto value was collected.


# uae-incountry-testing.csv

* url - URL that was being tested
* category_code - Category code as defined [here](https://github.com/citizenlab/test-lists)
* category_description - Description of the category
* secondary_category - If another category applies, it is included here
* access from UAE (du) - status of the URL (blocked or accessible)

# ye-incountry-testing.csv

* URL Category - Internal categorization annotation
* Accessibility from Yemen - Status of tests.

License
========

All data is provided under Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International and available in full
[here](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode) and summarized
[here](https://creativecommons.org/licenses/by-nc-sa/4.0/)
