
# === Install ===

install:
	@echo "Installing training pipeline..."
	
	poetry env use $(shell which python3) && \
	PYTHON_KEYRING_BACKEND=keyring.backends.null.Keyring poetry install && \
	poetry run pip install torch==2.0.1

# === Beam ===

export_requirements:
	@echo "Exporting requirements..."

	if [ -f requirements.txt ]; then rm requirements.txt; fi
	poetry export -f requirements.txt --output requirements.txt --without-hashes

upload_dataset_to_beam:
	@echo "Pushing data to the qa_dataset volume on Beam..."
	
	beam volume upload qa_dataset dataset


# === Training ===

dev_train_beam: export_requirements
	@echo "Running training pipeline on Beam using the development config..."

	BEAM_IGNORE_IMPORTS_OFF=true beam run ./tools/train_run.py:train -d '{"config_file": "configs/dev_training_config.yaml", "output_dir": "./output", "dataset_dir": "./qa_dataset/dataset", "env_file_path": ".env", "model_cache_dir": "./model_cache"}'

