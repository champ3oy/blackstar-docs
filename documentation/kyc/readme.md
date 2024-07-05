# KYC API Documentation

APIs for completing KYC for users

### Request Flow

Use this flow to get an idea of how the KYC flow works

1. #### Get KYC Questions

   Use this API to get all the questions for the KYC divided in sections and subSections.

   > [see documentation](https://blackstargroup.ai/developers?folder=kyc&page=getKYCQuetions)

2. #### Submit Answers

   This API is used to submit answers for questions by passing the question identifier and the answer in the supported type.

   ```json
    {
        "questionIdentifier": "answer",
        "questionIdentifier": "answer",
        ...
    }
   ```

   > [see documentation](https://blackstargroup.ai/developers?folder=kyc&page=addAnswers)

3. #### Upload File

   If a question requires a file such as Ghana Card Photo, Documents, etc use this API to upload the file. An ID is return, pass this ID to the

   > [see documentation](https://blackstargroup.ai/developers?folder=kyc&page=upload)

4. #### Delete File

   Use this API to delete an uploaded file. >[see documentation](https://blackstargroup.ai/developers?folder=kyc&page=deleteKYCDocument)

5. #### Submit KYC Form

   After adding all answers to the question, use this API to submit the KYC for review and verification.

   > [see documentation](https://blackstargroup.ai/developers?folder=kyc&page=submit)

6. #### Check KYC Verification Status
   This API takes a KYC ID and returns the verification status. >[see documentation](https://blackstargroup.ai/developers?folder=kyc&page=kycStatus)
