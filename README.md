# Blox-Assessment-Q1
## Emitting business metrics for Reference price match
### What did the system do?
The system provided an automated pricing feature for SKUs (Stock Keeping Units) in inventory. Users could match their prices with the lowest price, featured price, and competitive price using Match buttons alongside each price. These suggested prices, derived from calculations, aimed to help users increase their sales by being more competitive. Earlier there was no means to capture the business metrics. To capture and analyze the impact of these price changes, the system collected business metrics (e.g., old_price, new_price, old_shipping_price, new_shipping_price, old_points, new_points, last_modified_date, matched_reference_price, sku, asin etc.) and logged them into Andes table using a CommandEntry object. CommandEntry object describes the command to execute its parameters and which child id it is going to based on the destination field. It contains the name of the command(LOG_NEXUS_METRIC), command destination(SMP_CORE) and list of parameters with which the given command will run. We serialize the CommandEntry into a JSON response and return it.

### What other systems have you seen in the wild like that?
Similar systems I've seen include:

1) Dynamic Pricing Engines: Used in e-commerce platforms like eBay, where prices are adjusted in real-time based on competitor pricing, demand, and inventory levels.\
2) Ad Bidding Systems: Google AdWords and Facebook Ads where bids are dynamically adjusted based on competitor bids, budget, and performance metrics.\
3) Revenue Management Systems: Used by airlines and hotels to adjust pricing based on occupancy rates, booking patterns, and competitor pricing.

### How do you approach the development problem?
Requirement Gathering: Understand the functional and non-functional requirements by discussing with stakeholders.\
Design: Follow the system architecture, focusing on scalability and robustness.\
Implementation:\
Develop the feature in small, manageable modules and functions.\
Capture business metrics in a Map<String, Object> and pass it through the system to SaveDataRootController which further saves the request using CUBA. Logging the metrics into Andes table using CommandEntry object.\
Testing: Write unit tests to ensure the correctness of each module. And thoroughly test in Android and iOS for different versions.\
Deployment: Deploy the feature in a controlled environment and monitor its performance.

### What were interesting aspects where you copied code from Stack Overflow?
1) JSON Serialization Issues: When encountering the JSONParsingException with specific fields, I found a workaround on Stack Overflow that suggested wrapping problematic fields with escape characters to avoid parsing errors.\
2) Date Formatting: For formatting dates in a way that avoided serialization issues, I found a helpful example on Stack Overflow that used DateTimeFormatter with a specific pattern and applied it.

### What did you learn from some very specific copy-paste? Mention explicitly some of them.
1) Handling JSON Parsing Issues:\
This taught me how to handle special characters in JSON strings that could cause parsing issues, ensuring robust serialization.\
2) Date Formatting for JSON:\
Andes table required last_modified_date and timestamp in a specific format.\
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd'T'HH:mm:ss'Z'");\
This taught me how to format dates correctly to avoid serialization issues and ensure that date fields are properly handled in JSON objects.\


