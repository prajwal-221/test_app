# test_app
Version Control System
flowchart TD
    A["Incoming Workload"] --> B["ECS Tasks Consume More CPU/Memory"]

    B --> C{"Service CPU > 75% or Memory > 75%?"}

    C -- YES --> D["ECS Service Auto Scaling:
                    Add New Task(s)"]
    C -- NO --> Z["No scaling required"]

    D --> E{"Cluster Capacity Available?"}

    E -- YES --> F["Task Started Successfully"]
    E -- NO --> G["ASG Scaling Triggered:
                   • CPU > 85% or
                   • MemoryReservation > 85%
                   → Add EC2 Instance"]

    G --> H["New EC2 Instance Registered in ECS"]

    H --> I["New Tasks Can Now Run"]

    F --> J["Load Reduces"]
    J --> K["Scale Down Tasks Gradually"]

    I --> J
