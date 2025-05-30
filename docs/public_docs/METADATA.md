[ Overview](./README.md)

![plot](./images/linkedin.png)

### FeeWise metadata - in development
The ability to add metadata to FeeWise objects is currently in development. Check the roadmap for the latest status.

The majority of FeeWise objects, such as Invoice, PaymentLink, Trust Deposit and , Charge, Customer will soon come with a metadata parameter. 
The metadata parameter allows you to associate arbitrary key-value data with these FeeWise objects.

Metadata serves as a valuable means to store supplementary, organised data about an object. 
For instance, you have the option to store your own specific identifier from your system on a FeeWise Charge object. 
By default, FeeWise does not utilise metadata. However, the Search API will support metadata. Unless explicitly shown to users, metadata will remain hidden from their view.

Avoid storing any sensitive information in the metadata object.
