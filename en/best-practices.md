# Best practices

- Use Artisan CLI for creating classes.
- Use resource controllers for crud operations.
- Keep test coverage as high as possible (ideally 70-80%).
- Better duplicating code than create bad abstractions.
- Group classes into subfolders by resource.
- Keep controller methods thin.
- Models should contain only database related things.
- Use support classes for custom code logic.
- Never update the database directly, use migrations instead.
- Don’t modify migration files when the application is live, always create new migrations.
- Simplify the architecture with actions.
- Entities like states or types should be in Enums
- Observers should handle model events.
- Custom application settings be in own config - e.g. we have project.php
