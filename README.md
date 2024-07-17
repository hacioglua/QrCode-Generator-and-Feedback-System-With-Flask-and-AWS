# QR Code Verification and Feedback System with Flask (AWS RDS, EC2, S3)

This Flask application allows users to submit feedback after verifying their identity with a QR code. It includes functionalities for users, staff, and admins, leveraging AWS services for infrastructure.

## Features

- **User registration and login**
- **QR code upload and verification**
- **Feedback submission**
- **Staff view for uncommented feedback**
- **Admin view for all feedback with comments (if any)**

  ## User Interface
![](ScreenShoots/HomePage.jpeg)
![](ScreenShoots/LoginPage.jpeg)
![](ScreenShoots/Upload-QRCodePage.jpeg)
![](ScreenShoots/ProvideFeedbackPage.jpeg)
![](ScreenShoots/AdminPage.jpeg)
![](ScreenShoots/StaffPage.jpeg)

## Requirements

- Python 3
- Flask
- Flask-SQLAlchemy
- Flask-Bcrypt
- OpenCV-Python
- Werkzeug

## Deployment

This application is designed to be deployed on AWS:

### Database
- **Amazon RDS (Relational Database Service)** is used to store application data. You'll need to configure your database connection string accordingly.

### Server
- **Amazon EC2 (Elastic Compute Cloud)** provides a virtual server to run the Flask application.

### Storage
- **Amazon S3 (Simple Storage Service)** can be used to store uploaded QR code images (optional).

## Database Setup

1. Create an RDS database instance on AWS.
2. Define database credentials (username, password) securely.
3. Replace `'You should write your own db here'` in `app.config['SQLALCHEMY_DATABASE_URI']` with your actual RDS connection string.

## Deployment Steps

1. **Install required libraries on your EC2 instance.**
    ```bash
    pip install flask flask-sqlalchemy flask-bcrypt opencv-python werkzeug
    ```

2. **Save the code as `app.py`.**

3. **Configure your web server (e.g., Apache, Nginx) to serve the application from the EC2 instance.**

4. **Consider implementing environment variables to store sensitive information like database credentials.**

5. **For additional security, configure security groups on your EC2 instance to restrict access.**

## Optional S3 Integration

If you want to store uploaded QR code images in S3:

1. Configure AWS credentials for S3 access in your application.
2. Modify the `upload_qr` route to upload the QR code image to S3 instead of saving it locally.
3. Implement logic to retrieve the image from S3 for decoding.

## Application Overview

### Models
- **Users**: Stores user information (username, hashed password, role).
- **Feedback**: Stores user feedback along with username and user ID.
- **Comment**: Stores staff comments associated with specific feedback entries.

### Routes
- **User Registration and Login**
- **QR Code Upload and Verification**
- **Feedback Submission**
- **Staff View for Uncommented Feedback**
- **Admin View for All Feedback with Comments**

### QR Code Verification
- Use OpenCV for QR code detection and decoding.

### Security
- Password hashing with Flask-Bcrypt.
- Use Werkzeug for password hashing and security utilities.

## Note

- This is a basic implementation and can be further customized based on your specific requirements.
- Error handling can be improved to provide more informative feedback to users.
- Consider implementing additional security measures like CSRF protection in production environments.
- Email notifications for new feedback or comments can be added.

## Additional Resources

- **Deploying a Flask application on AWS**: [AWS Tutorial](https://aws.amazon.com/tutorials/serve-a-flask-app/)
- **Using S3 with Python**: [Boto3 Documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)
