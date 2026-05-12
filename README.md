# CYB125-ai-final-project
# Windows Security Baseline Script

## About This Project
# This project is aimed towards creating a security snapshot through a Python script. This will pull information from the Windows Registry, performance counters, and pieces of the command line to create a JSON file including a baseline with a dictionary for each important category. The main goal is to track any unauthorized changes on a system by comparing two snapshots, which would make finding the source of a breach much easier. This kind of tooling is useful for system administrators, security analysts, and anyone responsible for monitoring the integrity of a Windows machine over time.

## Approach
# The sources we will be collecting data from will be the Windows Registry, the performance counters, and various elements of the command line. From the registry, we will collect OS info, including the version of Windows being used and the build number. We will also collect installed services on the device, any applications that run on startup, group and security policies, and other data that may be altered. The performance counters will allow us to track memory usage that may have changed, as well as how the overall performance of the system may have shifted between snapshots. Command-line utilities will be used to gather additional system details such as user accounts, hotfixes, scheduled tasks, and network configuration that are more easily accessed through tools like net, schtasks, and netstat.

Data Dictionary
pythonbaseline = {
    "snapshot_metadata": {
        "schema_version": "",
        "timestamp_utc": "",
        "hostname": "",
        "generated_by_user": "",
        "elevated": "",
        "script_version": "",
        "python_version": "",
        "collection_duration_seconds": "",
        "collection_warnings": []
    },
    "system_identity": {
        "computer_name": "",
        "os_name": "",
        "os_build": "",
        "os_edition": "",
        "registered_owner": "",
        "registered_organization": "",
        "product_id": "",
        "os_version": "",
        "install_date_utc": "",
        "last_boot_utc": "",
        "uptime_seconds": "",
        "time_zone": "",
        "domain_or_workgroup": "",
        "is_domain_joined": ""
    },
    "hardware_profile": {
        "cpu": {
            "name": "",
            "manufacturer": "",
            "max_clock_mhz": "",
            "architecture": "",
            "logical_processors": "",
            "physical_cores": ""
        },
        "memory": {
            "total_physical_bytes": ""
        },
        "bios": {
            "manufacturer": "",
            "version": "",
            "release_date": ""
        },
        "system": {
            "manufacturer": "",
            "model": ""
        },
        "logical_disks": [
            {
                "drive_letter": "",
                "filesystem": "",
                "total_size_bytes": "",
                "free_space_bytes": ""
            }
        ]
    },
    "network_configuration": {
        "primary_dns_suffix": "",
        "adapters": [
            {
                "name": "",
                "description": "",
                "mac_address": "",
                "dhcp_enabled": "",
                "ipv4_addresses": [],
                "ipv4_subnet_mask": "",
                "default_gateway": "",
                "dns_servers": []
            }
        ]
    },
    "listening_ports": [
        {
            "protocol": "",
            "local_address": "",
            "local_port": "",
            "state": "",
            "owning_pid": "",
            "owning_process_name": ""
        }
    ],
    "local_user_accounts": {
        "current_user": "",
        "users": [
            {
                "username": "",
                "full_name": "",
                "sid": "",
                "disabled": "",
                "password_required": "",
                "password_changeable": "",
                "password_expires": "",
                "last_logon_utc": ""
            }
        ],
        "administrators_group_members": []
    },
    "password_policy": {
        "minimum_password_length": "",
        "minimum_password_age_days": "",
        "maximum_password_age_days": "",
        "password_history_length": "",
        "lockout_threshold": "",
        "lockout_duration_minutes": "",
        "lockout_observation_window_minutes": "",
        "force_logoff_after_minutes": ""
    },
    "auto_start_services": [
        {
            "name": "",
            "display_name": "",
            "state": "",
            "start_type": "",
            "executable_path": "",
            "log_on_as": ""
        }
    ],
    "running_processes": [
        {
            "pid": "",
            "parent_pid": "",
            "name": "",
            "executable_path": "",
            "command_line": ""
        }
    ],
    "installed_software": [
        {
            "display_name": "",
            "display_version": "",
            "publisher": "",
            "install_date": "",
            "registry_hive": "",
            "is_64_bit": ""
        }
    ],
    "installed_hotfixes": [
        {
            "hotfix_id": "",
            "description": "",
            "installed_on": "",
            "installed_by": ""
        }
    ],
    "persistence_locations": {
        "hklm_run": [
            {
                "name": "",
                "value": ""
            }
        ],
        "hkcu_run": [
            {
                "name": "",
                "value": ""
            }
        ],
        "hklm_run_once": [],
        "hkcu_run_once": [
            {
                "name": "",
                "value": ""
            }
        ],
        "all_users_startup_folder": {
            "path": "",
            "files": []
        },
        "current_user_startup_folder": {
            "path": "",
            "files": []
        }
    },
    "scheduled_tasks": [
        {
            "task_name": "",
            "status": "",
            "next_run_time": "",
            "last_run_time": "",
            "last_result": "",
            "author": "",
            "task_to_run": ""
        }
    ],
    "security_posture": {
        "firewall": {
            "domain_profile": {
                "state": "",
                "default_inbound_action": "",
                "default_outbound_action": "",
                "logging_dropped_connections": ""
            },
            "private_profile": {
                "state": "",
                "default_inbound_action": "",
                "default_outbound_action": "",
                "logging_dropped_connections": ""
            },
            "public_profile": {
                "state": "",
                "default_inbound_action": "",
                "default_outbound_action": "",
                "logging_dropped_connections": ""
            }
        },
        "windows_defender": {
            "antivirus_enabled": "",
            "real_time_protection_enabled": "",
            "antivirus_signature_age_days": "",
            "antivirus_signature_version": ""
        },
        "uac": {
            "enabled": "",
            "consent_prompt_behavior_admin": "",
            "prompt_on_secure_desktop": ""
        },
        "bitlocker": {
            "system_drive_protection_status": "",
            "encryption_method": "",
            "encryption_percentage": ""
        }
    },
    "performance_snapshot": {
        "sample_timestamp_utc": "",
        "cpu_total_percent": "",
        "memory": {
            "available_bytes": ""
        },
        "disk_system_volume": {
            "reads_per_sec": "",
            "writes_per_sec": ""
        },
        "process_count": ""
    },
    "network_shares": [
        {
            "share_name": "",
            "local_path": "",
            "description": "",
            "is_administrative": ""
        }
    ]
}

## Configuration Areas

# snapshot_metadata — Records when and how the snapshot was taken, including the script version, Python version, and runtime warnings, so that any two snapshots can be meaningfully compared and traced back to their collection context.
# system_identity — Captures core identifiers of the machine such as hostname, OS version, architecture, and domain membership, which establishes a verified fingerprint of the system at the time of collection.
# hardware_profile — Documents physical and virtual hardware specifications including CPU, RAM, disk, and firmware details, allowing detection of unauthorized hardware changes or virtualization anomalies.
# network_configuration — Records network interface settings, IP addresses, DNS servers, and default gateways, which is critical for identifying rogue interfaces or DNS hijacking between snapshots.
# listening_ports — Catalogs active ports and sockets awaiting inbound connections mapped to their owning processes, making it possible to spot unexpected or malicious services exposing network access.
# local_user_accounts — Enumerates locally defined user accounts, their privilege levels, group memberships, and account status so that unauthorized account creation or privilege escalation can be detected.
# password_policy — Documents the enforced rules governing password complexity, expiration, history, and lockout thresholds, which reveals whether security policies have been weakened between snapshots.
# auto_start_services — Lists system services configured to launch automatically on boot or login, since attackers frequently install malicious services to maintain persistent access across reboots.
# running_processes — Captures currently active processes in memory including their PIDs, parent relationships, and executable paths, enabling identification of suspicious or injected processes at the time of collection.
# installed_software — Provides an inventory of all applications and packages on the system with versions and install dates, making it straightforward to spot unauthorized software installations or removals.
# installed_hotfixes — Logs applied OS patches and security updates with their timestamps, which is essential for verifying patch compliance and identifying systems that are missing critical updates.
# persistence_locations — Collects registry Run keys, startup folders, and other mechanisms that allow programs to survive reboots, as these are among the most common hiding spots for malware persistence.
# scheduled_tasks — Records time- and event-triggered jobs including their triggers and run-as context, since attackers commonly abuse scheduled tasks to execute code automatically without user interaction.
# security_posture — Captures the state of key security controls such as Windows Defender, UAC, firewall profiles, and BitLocker, providing a quick-reference view of whether protective mechanisms are active and properly configured.
# performance_snapshot — Takes a point-in-time capture of CPU load, available memory, disk I/O, and process count, which can reveal resource abuse or hidden workloads introduced between baseline comparisons.
# network_shares — Enumerates shared folders exposed over the network including administrative shares, since unauthorized shares can expose sensitive data or serve as lateral movement paths for an attacker.


## Strategy
# To complete this assignment, I will go step by step with the AI assistant, having it read through the README file along with providing extra direction in order to guide it into producing the code necessary to generate the JSON output file with the correct dictionary and nested keys. Using the foundational knowledge obtained through the semester, I will direct the AI on what code will be used and where, rather than allowing it to make those architectural decisions independently. I will only have it expand on ideas that I provide, not generate its own, which keeps the output mostly human-directed and only written out by the AI. The milestone where I expect AI assistance to be most useful is the registry collection section, since the winreg module has specific syntax that benefits from targeted explanation. The milestone where I plan to rely on it least is the data dictionary structure itself, since that design comes directly from understanding the project requirements and the example output file.

## Milestones
# The project is structured around eight milestones, each one designed to produce a working JSON file with an additional section implemented. The milestone structure isn't just a grading convenience, it's a deliberate AI-collaboration pattern.
# When students use AI well, they treat it like a pair programmer: they bring it small, well-scoped problems, ask it to explain things rather than just produce things, and verify its answers against an authoritative source (the textbook, the official Python docs, or their own running code). The output is code they understand and could rewrite from scratch.
# The eight-milestone structure exists to force the second pattern. Each milestone is small enough that you can hold the whole thing in your head. Each milestone has a specific Python concept attached to it, so you know what you're supposed to be learning. Each milestone has a suggested AI prompt that asks for explanation, not code.
# Your goal is not to finish the project as fast as possible. Your goal is to finish the project understanding what you built. Those are different goals. The milestone structure pushes you toward the second one.