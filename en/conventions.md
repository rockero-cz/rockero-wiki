# Naming Conventions

| Class        | Naming                                                     | Example                                                                              |
| ------------ | ---------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Action       | action name with “Action” suffix                           | `CreateUserAction`, `DeleteProductAction`, `UpdateCategoryAction`                    |
| Command      | command name without suffix                                | `GenerateReport`, `ImportData`, `ExportData`                                         |
| Controller   | singular with “Controller” suffix                          | `UserController`, `ProductController`, `CategoryController`                          |
| Data         | singular with “Data” suffix                                | `UserData`, `ProductData`, `CategoryData`                                            |
| Event        | event name without suffix                                  | `UserCreated`, `OrderCreated`, `OrderShipped`                                        |
| Exception    | singular with “Exception” suffix                           | `ValidationException`, `NotFoundException`, `DuplicateEntryException`                |
| Interface    | adjective/noun without suffix                              | `Loggable`, `Configurable`, `Exportable`                                             |
| Job          | job name without suffix                                    | `SendEmailJob`, `ProcessPaymentJob`, `GenerateReportJob`                             |
| Mail         | mail name without suffix                                   | `WelcomeEmail`, `OrderConfirmationMail`, `NewsletterMail`                            |
| Middleware   | middleware name without suffix                             | `Authentication`, `RateLimit`, `Cors`                                                |
| Model        | singular without suffix                                    | `User`, `Product`, `Category`                                                        |
| Notification | notification name without suffix                           | `InvoicePaid`, `OrderShipped`, `PasswordReset`                                       |
| Observer     | singular model name with “Observer” suffix                 | `UserObserver`, `ProductObserver`, `CategoryObserver`                                |
| Policy       | singular model name with “Policy” suffix                   | `UserPolicy`, `ProductPolicy`, `CategoryPolicy`                                      |
| Provider     | provider name with “Provider” suffix                       | `PaymentProvider`, `StorageProvider`, `EmailProvider`                                |
| Request      | method name with singular model name with “Request” suffix | `StoreUserRequest`, `UpdateProductRequest`, `DestroyCategoryRequest`                 |
| Rule         | rule name without suffix                                   | `ValidPhoneNumber`, `ValidBankAccount`, `Uppercase`                                  |
| Scope        | scope name with “Scope” suffix                             | `ActiveScope`, `NewScope`, `TrendingScope`                                           |
| Support      | support name without suffix                                | `OpeningHours`, `Cart`, `Table`                                                      |
| Trait        | adjective/prefix “with“ without suffix                     | `Sortable`, `Searchable`, `Filterable`, `WithForm`, `WithSorting`, `WithFileUploads` |
