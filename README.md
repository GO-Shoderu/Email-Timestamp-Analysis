# Email-Timestamp-Analysis
This repository contains the code and documentation for an in-depth analysis of email timestamps. The analysis explores the reliability of email timestamps, uncovers outliers in email processing times, and investigates factors that influence delays in email delivery. The repository provides detailed insights into the data extraction process, data cleaning, statistical analysis, and visualizations. It serves as a valuable resource for anyone interested in understanding the intricacies of email communication and the factors that affect the timing of email delivery.

# Experimental Setup
I obtained the emails for this analysis from my personal Gmail account, specifically go.shoderu@gmail.com, which I have been actively using since its creation in 2021. To facilitate manageable data handling, I initiated the process by extracting a preliminary dataset of approximately 4,890 emails. These emails were identified based on a specific keyword search for "noreply@." Subsequently, I conducted a random selection process to pick a representative sample of 100 emails for in-depth analysis.

The task of extracting emails was effectively carried out using the Thunderbird email client. Thunderbird provided a seamless means of acquiring email data from my Gmail account while meticulously preserving the original email format. It's noteworthy that all extracted emails were saved in ".eml" file format to ensure that the native structure of each email was retained throughout the process.

Central to my analysis was a detailed examination of email headers, with a particular emphasis on the extraction of vital metadata. Python emerged as the programming language of choice for data processing, to better visualize what I am working with, I made use of the Jupyter notebook, leveraging the "email" library to extract essential header information. Key elements like "From," "Sent," "X-Received," and various "Received" header details were meticulously collected.

Additionally, I employed the Python "re" library, which played a pivotal role in the extraction of date and time information, including the associated time zones, from the headers of each email. This rigorous data preparation process resulted in a well-structured dataset, encompassing the email headers and timestamps crucial for subsequent analysis.

In the crucial stage of the analysis, I compiled the extracted data into a structured .csv file. This .csv file serves as the foundational data source for my subsequent data analysis endeavors. Its structured format facilitates ease of access to the extracted metadata, allowing for a comprehensive exploration of the email timestamps and headers.
The meticulous steps involved in the data preparation process were as follows:
  1.	Extraction of date and time header information, which was then stored in a structured .csv file named "100_email.csv." Each email's header information was allocated its dedicated column within the file. This is shown in figure 1.
  2.	Addressing inconsistencies in the date and time information, such as variations in time zones represented as figures (e.g., "-0700"), in words (e.g., "(PDT)"), or a combination of both. After rectifying these inconsistencies, the cleaned data was stored in a file labeled "100_email_cleaned.csv."
  3.	Realizing that all emails in the dataset shared the same date, I made the decision to focus solely on the time and time zones. Subsequently, I stored this refined data in the "100_email_with_time_and_timezone.csv" file.
  4.	The "pytz" library was employed to extract time and time zone information and generate a new timestamp in South African time. This processed data was then saved in the "100_email_with_time_to_sa.csv" file.
  5.	To calculate the time interval between an email's dispatch and reception, I determined the time the email was sent and subtracted it from the highest timestamp recorded among the X-Received and other Received time entries. The final output was saved as "100_email_with_time_difference.csv" as shown in figure 2.

Throughout this experimental setup, I maintained a commitment to executing the sourcing, extraction, and processing of the email dataset with the utmost care and precision. The "100_email_with_time_difference.csv" file now stands as the primary dataset for further investigation and analysis. 

This structured dataset serves as a valuable foundation for my subsequent research and analysis.

![Figure 1](https://github.com/GO-Shoderu/Email-Timestamp-Analysis/assets/85843032/2a581ed1-3169-47df-8e8c-97bac8ca1404)

![Figure 2](https://github.com/GO-Shoderu/Email-Timestamp-Analysis/assets/85843032/a1e244c3-622c-49ee-8076-5c7388907726)

# Observations
In the analysis of the timestamps associated with the emails, several key observations emerged. The following table summarizes key statistical measures for time differences in the dataset:

| Statistical Measure  | Value |
| ------------- | ------------- |
| Count  | 100 emails  |
| Mean  | 1.44 seconds  |	
| Standard Deviation | 1.17 seconds |
| Minimum	| 0 second |
| 25th Percentile	| 1 second |
| Median (50th Percentile) |	1 second |
| 75th Percentile |	2 seconds |
| Maximum	| 5 seconds |

The above statistics was calculated using the .describe() from the “pandas” library. The analysis of email time differences within a dataset of 100 emails reveals insightful patterns. On average, emails traverse from sender to recipient in approximately 1.44 seconds, indicating efficient and timely communication. However, a standard deviation of 1.17 seconds highlights variability, influenced by factors like network congestion and server performance.

![Figure 3](https://github.com/GO-Shoderu/Email-Timestamp-Analysis/assets/85843032/9624de95-4695-409c-a358-e5771a71a0ec)

Notably, as shown in figure 3 as a support to the table shown above, some emails were delivered instantaneously, with a minimum time difference of 0 seconds, showcasing the diversity of experiences. The median delivery time is 1 second, closely matching the mean. This suggests that most emails arrive quickly. The 25th percentile is also 1 second, indicating a significant number of swift deliveries. In contrast, the upper quartile at 2 seconds shows that some emails experience slightly longer delivery times.

The maximum time difference recorded is 5 seconds, signifying occasional delays. These observations illustrate the range of email delivery experiences, from near-instant to slightly delayed. The dataset provides valuable insights into email transmission efficiency and the factors influencing delivery times.

# Outliers
The analysis exposed outliers in email processing times, ranging from 4 to 5 seconds, indicating extended transmission periods in certain emails compared to the majority.

![Figure 4](https://github.com/GO-Shoderu/Email-Timestamp-Analysis/assets/85843032/32f6b6da-f58b-4ab8-9b59-a4c197a25799)

The box plot in Figure 4 clarifies this, displaying an average processing time between 1 and 2 seconds and marking the identified outliers.

Upon closer examination of the emails, categorized by time intervals starting from 0 seconds, it was initially tempting to attribute the outliers to time zone differences. However, a more comprehensive analysis revealed that while time zones may contribute, they do not solely account for the variations.

These outliers could be influenced by various factors, including complex email routing and intermediate processing. Emails passing through multiple Mail Transfer Agents (MTAs) or servers may encounter delays due to network congestion or server inefficiencies, leading to the observed outliers.

Additionally, recipient-specific configurations, such as spam filters and custom routing rules, can introduce delays for specific emails, contributing to the outliers.

![Figure 5](https://github.com/GO-Shoderu/Email-Timestamp-Analysis/assets/85843032/64c906a3-2e3b-4058-b2c8-5802e8f683b0)

The distribution of time differences exhibits positive skewness, with a tail towards longer processing times as shown in figure 5, signifying the presence of emails with extended transmission durations alongside promptly delivered ones.

# Conclusion
In conclusion, based on my experimental observations, I've gained insights into the reliability of email timestamps. The statistics from the analysis serve as a foundation for discussing the consistency and occasional anomalies in email timestamps.

The time differences revealed an average of 1.44 seconds and a standard deviation of 1.17 seconds. This indicates that email timestamps are generally dependable, as most emails exhibited prompt delivery, with 75% of them having time differences of 2 seconds or less. It suggests that email timestamps are a reliable means to assess email delivery times. Nevertheless, the presence of outliers with time differences of 4 to 5 seconds raises questions about the reliability of timestamps in specific cases.

My observations also highlight potential challenges in consistently relying on email timestamps. While email headers typically contain timestamp information, I encountered problematic cases where time was not included in a usable format. Some inconsistencies stemmed from variations in time zones, including numeric representations and abbreviations such as "PDT." These inconsistencies underscore the importance of standardized timestamp formats to enhance the reliability of email timestamps.

In summary, my analysis suggests that email timestamps are generally reliable for assessing email delivery times, supported by the statistical findings. However, the presence of outliers and inconsistencies in timestamp formats underscores the need for improved standardization and verification of email timestamps to ensure consistent and accurate time tracking in email communication.

I have created a drive containing all the files I extracted from my email, I stored them in a folder called “resources”, they are around 4800+ and all the files I worked with for the analysis, which I limited to 100 emails, I stored them in a folder called “files”. The code I used in making sure I came to this conclusion is named “code.ipynb”. All the .csv files are also present in this drive. 
