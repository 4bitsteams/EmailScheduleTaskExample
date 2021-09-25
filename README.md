# Task Schedule Example as like cron job (Use Quartz Task Schedule Package)

it is class library you have to add you project and just call it in your Startup.cs

          // Add Quartz services
            services.AddHostedService<QuartzHostedService>();
            services.AddSingleton<IJobFactory, SingletonJobFactory>();
            services.AddSingleton<ISchedulerFactory, StdSchedulerFactory>();

            // Add our job
            services.AddSingleton<RemindersJob>();
            services.AddSingleton<EmailReminderJob>();

            services.AddSingleton(new JobSchedule(
                jobType: typeof(RemindersJob),
                cronExpression: "0/30 0/1 * 1/1 * ? *")); // run every 5 min

            services.AddSingleton(new JobSchedule(
               jobType: typeof(EmailReminderJob),
               cronExpression: "0/30 0/1 * 1/1 * ? *")); // run every 5 min
