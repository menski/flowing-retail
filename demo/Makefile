.PHONY: infra
infra:
	docker-compose -f infra.yaml up -d
	sleep 2
	zbctl deploy order-tracking.bpmn

.PHONY: tracking
tracking: clean-orchestrate
	docker-compose -f tracking.yaml up -d
	sleep 1
	docker pause demo_inventory_1

.PHONY: orchestrate
orchestrate: clean-tracking
	docker-compose -f orchestrate.yaml up -d
	sleep 1
	docker pause demo_inventory_1

.PHONY: fix
fix:
	docker unpause demo_inventory_1

.PHONY: clean
clean: clean-tracking clean-orchestrate
	-docker-compose -f infra.yaml down -v

.PHONY: clean-tracking
clean-tracking:
	-docker-compose -f tracking.yaml down -v

.PHONY: clean-orchestrate
clean-orchestrate:
	-docker-compose -f orchestrate.yaml down -v
