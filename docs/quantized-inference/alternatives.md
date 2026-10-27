# Appendix: the four competing approaches and how they were judged

Four independent designs were produced from different angles, scored by three judges (seed investor, ML-systems engineer, GTM operator), then the winner was stress-tested by three adversarial reviewers. The vertical (Sankshep) and the developer tool (quantc) finished within one point of each other on the judges' tally; the adversarial review is what pushed the final brief toward the narrow vertical. The devtool design is kept here in full because it is the closest to a literal "quantization-first Simplismart".

## Judge scores (1-10 per criterion, 50 max per judge)

| Judge | Design | Feasibility (small team) | Technical differentiation | Market timing | Defensibility | Capital efficiency | Total |
|---|---|---|---|---|---|---|---|
| 1 | quantc (devtool) | 7 | 6 | 7 | 4 | 7 | 31 |
| 1 | Fewbit (edge) | 4 | 5 | 5 | 4 | 5 | 23 |
| 1 | Nibble (serving) | 6 | 4 | 6 | 3 | 5 | 24 |
| 1 | Sankshep (vertical) | 4 | 7 | 7 | 6 | 6 | 30 |
| 2 | devtool (quantc) | 7 | 5 | 6 | 4 | 7 | 29 |
| 2 | vertical (Sankshep) | 5 | 6 | 7 | 6 | 6 | 30 |
| 2 | edge (Fewbit) | 4 | 6 | 5 | 5 | 5 | 25 |
| 2 | serving (Nibble) | 5 | 4 | 6 | 4 | 4 | 23 |
| 3 | quantc (devtool) | 7 | 6 | 6 | 4 | 7 | 30 |
| 3 | Fewbit (edge) | 5 | 6 | 4 | 5 | 6 | 26 |
| 3 | Nibble (serving) | 6 | 5 | 7 | 4 | 5 | 27 |
| 3 | Sankshep (vertical) | 5 | 7 | 7 | 6 | 7 | 32 |

### Judge 1 — winner: quantc (devtool)

- **quantc (devtool)** (31): Feasibility: the minimum sellable unit (Typer CLI over llm-compressor 0.14 + AutoRound + lm-eval 0.4.13 + GuideLLM, a signed quantcard, an HF org, and a Rs 3-5 lakh audit engagement) is 3-4 weeks of wrapper work for a Python founder, and it is exactly the job Simplismart did bespoke for Sanas (Gemma-3 INT4, H100->A10G). The 8-week plan as written is overloaded (hosted control plane, Stripe/Razorpay, GitHub Action, nightly drift, ModelOpt/B200 adapter, 12 published models, 10 design partners, 300 stars) and will slip; weeks 5-6 should be cut. Differentiation: the synthesis (fleet-aware planner, KL/CoT-length/tool-call gates, per-SM compat table, pinned toolchains, card) is real, but every primitive exists: ModelOpt AutoQuantize searches NVFP4/FP8/BF16 under effective_bits (Aug 2026) and KV AutoQuant shipped Oct 2026, AutoRound AutoScheme, llm-compressor HIGGS, Intel INC tolerable_loss. Timing: tool consolidation (AutoAWQ/AutoGPTQ dead, quanto/TorchAO winding down) and 'silent quantization' governance complaints are real, but the auto-search window is closing while the neutral-card window is open. Defensibility: thinnest of the credible options; Red Hat or NVIDIA can ship a free 'quantize with gate' CLI, and the comps are brutal (Nota ~$5.9M revenue at a $462M IPO, Pruna ~$2.8M on a $6.5M seed). $29/build and $399/mo Team pricing is hobbyist-scale; the design's own 12-month target is $150-250k ARR. Capital: ~$3-5k of rented GPU for 8 weeks, no hardware, no on-call, $300-400k to 12 months; complementary to serving clouds rather than fighting the $0.05-0.14/M token floor.
- **Fewbit (edge)** (23): Feasibility: the 8-week plan asks two people to ship a C++ core over llama.cpp, Kotlin/JNI and Swift xcframework SDKs, a Python SDK, ExecuTorch QNN 16a4w, MLX and Olive/ONNX exports, OTA with resumable signed downloads, telemetry, a dashboard and a control plane, plus buy and automate a 15-device rack. The founder profile is Python/FastAPI; the critical hire is a native mobile engineer the design itself says the product dies without. Edge toolchains are the worst in the digest: Qualcomm GenieX is 'developer preview' with Gemma-4 E4B accuracy issues, a Qwen3-0.6B W4A16 conversion took ~77 minutes, Ollama/LM Studio do not use NPUs at all. Differentiation: per-SoC certification and a manifest resolver are a sensible workflow, but no kernels, no algorithms, and Ollama ($65M, 8.9M devs), NimbleEdge, Cactus, Nexa and Picovoice already sit here. Timing: Gemma 4 QAT and ExecuTorch 1.5 help, but Apple Foundation Models, Gemini Nano/AICore and Qualcomm (Edge Impulse + Modular) are making the generic path free, and the India mass-market thesis collides with 6 GB Dimensity phones doing 3-8 tok/s with thermal throttling, so the product risks being flagship-only. Defensibility: the design admits 'at month 8 the moat is zero'; the device x model x quant corpus is the long-run asset but takes 12+ months. Capital: Rs 6-7 lakh rack, ~$8-10k/month burn is fine, but the buyer (Head of Mobile at a tens-of-rupees-ARPU Indian app) is the stingiest in the set, $0.005/MAD pricing competes with $0.006/user/month cloud tokens, and OEM pre-install deals (Micromax/Lava/Jio) are multi-year. Hardest of the four to turn into revenue inside 6 months.
- **Nibble (serving)** (24): Feasibility: technically the easiest stack (vLLM 0.20 + llm-compressor + Helm/k3s on an E2E L40S + FastAPI gateway + Razorpay) and a single endpoint with a card is a 4-week job, but the product is a serving platform with 99.5% uptime, precision-pin and accuracy-floor SLAs, weekly drift shadows, BYOC agent in Go and an air-gapped bundle; the design concedes 'solo on-call is not credible' and makes an SRE hire a hard dependency by month 2-3. Differentiation: lowest in the set; the planner rules, OpenAI gateway, Helm chart and card are 'copyable in weeks' by its own admission, and Simplismart (58 people, NVIDIA/Accel/DVC, $14M fresh) or Baseten can add precision headers in a sprint. Timing: cheap Ada/Ampere in India (L4 Rs 49/hr, L40S $1.20, A100-80 $2.10) with settled FP8/INT8 evidence (Red Hat L40S 576->830 tok/s) is a real wedge and Simplismart is >50% US revenue, but the lane is crowded: Inferless, Turiyam ($4M), Pipeshift x Neysa sovereign inference (May 2026), Yotta on Simplismart. This is the mini-Simplismart the research digest explicitly warns against. Defensibility: the ledger and regulated installs are the only assets; 'India capacity economics' require Rs 20-40 lakh prepaid commits that a pre-seed team cannot make, and a customer can rent the same E2E L40S at $1.20 and run the same vLLM FP8 recipe themselves. Capital: managed tier is GPU pass-through at ~35-45% gross margin, pilot endpoints are run at cost, mid-market ACVs are $1-5k/month so ~60-100 endpoints are needed for $1M ARR; serving businesses that win (DeepInfra, Baseten) own GPUs and raise hundreds of millions. It does sell the fastest ('cut your GPU bill 40-70% or pay nothing' against an existing line item), which is why it is not last.
- **Sankshep (vertical)** (30): Feasibility: this is three products (ASR, LLM, TTS) plus telephony (8 kHz mu-law, Exotel/Ozonetel/Asterisk adapters, Pipecat), diarization, PII redaction, QA rubrics, a gate, Helm, an air-gap bundle and a 30-audio-hour annotation program, in 8 weeks, with a founder plus one speech engineer. The design admits Mode B slips to a demo video. Worse, the binding constraint is outside the thesis: IndicWhisper is still 26.8% WER on GramVaani and code-mixed Hinglish is worse, so an 8 kHz fine-tune, not quantization, decides whether the voice pitch works; several load-bearing numbers (Sarvam API prices, DPDP dates, IndicF5/Parler/Voxtral licenses) are flagged '(verify)'. Differentiation: highest in the set; whole-path quantization (CTranslate2 int8_float16 ASR, Kokoro ONNX int8 TTS, FP8/INT8 KV with the explicit 24 GB-card concurrency math), the IndicCalib-v1 calibration hypothesis against the documented -3.8 to -4.7 pt Indic INT4 tax, per-language rather than English-average gates, and a script-integrity gate are things nobody (Sarvam, Simplismart, Unsloth) publishes. Timing: DPDP Rules, RBI FREE-AI (Aug 2025), Apache-2.0 Sarvam models and Rs 3-5/min human agents vs Rs 1.5-3/min cloud APIs make the Rs 0.30/min target a real budget line; counter-signal is that many banks already accept Mumbai VPCs. Defensibility: strongest of the four (BharatVoiceEval consented telephony sets, auditor-accepted Eval Cards, CCaaS embedding) and a niche no US vendor will enter; Sarvam with 4,096 subsidised H100s and existing on-prem offers is the real threat, and Gnani/Skit/Yellow are simultaneously customers and competitors. Capital: Rs 7-11 lakh for 8 weeks and Rs 1-1.3 Cr/yr is lean and Rs 3-5 lakh Mode A (batch call QA) pilots with BPOs can fund it, but BFSI direct sales mean 6-12 month cycles, vendor empanelment, VAPT/ISO 27001 before revenue, which contradicts 'sell in 6 months'. Also note it drifts from the user's question: quantization is the enabler here, not the product.

Ideas worth grafting:
- From Nibble: add the 'card-only SKU' ($299 standard suites / $999 with the customer's own eval set) as the top-of-funnel product from week 4, since it monetizes the gate without hosting anything and seeds the eval-set relationship; quantc's $29/build pricing is too low to matter.
- From Nibble: run a public precision ledger as the growth loop: every notable open-model release (Qwen, Gemma, Llama, Sarvam, gpt-oss) gets FP8 / INT8 W8A8 / W4A16 quantcards on L4, L40S and A100 within 48 hours, posted to r/LocalLLaMA and HN as reproducible GuideLLM runs with exact flags, explicitly contrasted with vendor single-user peaks (Simplismart's 501 vs 350 vs 343 tok/s).
- From Nibble: adopt GOLD/SILVER grading (mean recovery >=99.0% and min task >=97.0% vs >=98%/>=95%), a weekly 'last verified' drift block (500 sampled prompts replayed against a cached BF16 shadow for ~$4/week/model), and x-precision / x-recipe / x-card response headers that any host can emit from a quantc artifact; and write the precision-pin + accuracy-floor contract language as an optional enterprise addendum with credits capped at fees and precision-drift-only liability.
- From Nibble: record the speculative-decoding policy and measured draft acceptance in the quantcard and serve.sh (sequential 2-3-token drafts on W4A16 targets per SpecMQuant, EAGLE-3 trees only on FP8/INT8 targets, auto-disable below 1.15x at the endpoint's median batch), because the artifact's economics on L4/A10G depend on it.
- From Sankshep: build IndicCalib-v1 (Hindi/Hinglish/Tamil/Marathi/Indian English + JSON tool traces + numeral-heavy text, 1,024 x 2,048 chat-templated samples, published hash) and run the H1 experiment, publishing 'The Indic INT4 tax, measured' (6 models x 4 precisions x 4 languages x 3 GPUs) as quantc's first benchmark post instead of the generic '12 models, 3 cheap GPUs' post; it is the one datapoint nobody (Sarvam, Simplismart, Unsloth, RedHatAI) has, and it is the door-opener for the Sarvam, voice-ISV and BFSI calls already on quantc's list.
- From Sankshep: make the multilingual gate per-language (MILU per-language subsets, IndicGenBench/Flores-In chrF) rather than an English-average gate, and add a script-integrity gate (mojibake / wrong-script / repetition-collapse rate <= 0.1%) which is the documented failure mode for non-Latin scripts in quantized small models.
- From Sankshep: add two thin adapters for the rest of the voice path, CTranslate2 int8_float16 / int8 for Whisper-family ASR (with VAD gating, no temperature fallback and a hallucination-on-silence gate) and onnxruntime int8 for sherpa-onnx conformers and Kokoro TTS, so voice-agent design partners (Sanas/Gnani/Skit-class, already on quantc's call list) get the whole 24 GB-card budget audited, not just the LLM.
- From Sankshep: adopt the explicit per-call KV/VRAM arithmetic in `quantc plan` output (e.g. Llama-3.1-8B = 128 KiB/token so ~60 concurrent 2k-token calls at FP16 KV vs ~120 at FP8 KV on a 24 GB L4; Gemma head_dim-256 doubles it and needs sliding-window skip), and format the quantcard as a PDF Eval Card plus a one-page validation runbook written for RBI FREE-AI / DPDP model-risk reviewers, which is what turns a card into an enterprise-runner sale.
- From Sankshep: pick a batch call-QA BPO/CCaaS workload (Startek/Exotel-class) as one of the 10 design partners, because overnight batch scoring on T4/L4/CPU is the lowest-risk, highest-ROI place to prove a quantized artifact (no live-call latency risk, pure rupees per audio-minute).
- From Fewbit: publish a 'Can I run it?' matrix extended to GPUs (SKU x model x precision -> tok/s at the declared concurrency, go/no-go, $/M tokens) as the hub's hero asset, and borrow its perf-gate rigor (sustained 5-minute decode, peak RSS, thermal throttle, TTFT at 2048-token prompt) instead of a single GuideLLM sweep.
- From Fewbit: promote QAD for <=4B customer fine-tunes from 'phase 2' to a paid tier-2 service in month 3 (BF16 fine-tune as teacher, torchao QATConfig or llm-compressor QADModifier, 1-5k steps, ~$25-100 of H100 per model, export Q4_0 GGUF / 8da4w / w4a16), because PTQ will fail the gate most often on exactly the small models customers want on L4/A10G and phones.
- From Fewbit: treat LoRA adapters as first-class artifacts (merge-then-quantize vs base + runtime GGUF/vLLM adapter, both carded) and add the GGUF + KleidiAI Android/Arm-server path as the cheapest edge target in months 3-4, with the Mac mini / one Snapdragon phone / Orin Nano rack ($1-2k, not the full Rs 6-7 lakh) for the perf gate.
- From Nibble and Sankshep: bill in INR via Razorpay alongside Stripe, apply for IndiaAI Mission subsidised compute (Rs 67-92/GPU-hr) and NVIDIA Inception credits in week 1, and list quantc-certified artifacts in the E2E TIR / Jarvislabs / Neysa marketplaces as the India channel.
- Scope correction drawn from all three losers' honesty: cut quantc's weeks 5-6 (hosted control plane, CI action, nightly drift, ModelOpt/B200 adapter) and replace them with paid audit engagements, the Indic benchmark and the ledger; hosted search and the GitHub Action come only after 3 paying audits prove the card is what buyers want.

### Judge 2 — winner: vertical (Sankshep)

- **devtool (quantc)** (29): Most buildable and cheapest of the four (no owned GPUs; ~$15-25k for 8 weeks, $300-400k for 12 months) and the hardware DB is correct where it matters: no FP8 W8A8 on A100/A10G, NVFP4 = Marlin W4A16 memory-only on Hopper, W4A16 gives no throughput over W8A8 on H100, SM120 flagged unstable (TRT-LLM #14154, llama.cpp #26704 still open). But the 'compiler' is glue over four vendor toolkits whose owners already ship the search it claims: ModelOpt AutoQuantize (effective_bits over NVFP4/FP8/BF16, Aug 2026) and KV AutoQuant (Oct 2026), AutoRound AutoScheme, llm-compressor HIGGS ILP, Intel INC tolerable_loss autotune. What remains (cross-toolkit GGUF/ExecuTorch export, customer-eval gates incl. CoT-length <=1.10x, tool-call JSON and per-language sub-gates, the quantcard, CI gate, pinned toolchains with nightly drift rebuilds) is real and absent from vendor tools, but Red Hat could ship it as `llmcompressor gate` in a quarter and it is Apache-2.0 by design. The HQQ/RTN-proxy per-block KL sensitivity scan is methodologically weak (RTN layer sensitivity does not transfer reliably to GPTQ-optimized layers); the promote-on-failure loop is the actual mechanism, i.e. brute force. The 8-week plan (four adapters, control plane, CI action, drift, NVFP4 on rented B200s, 12 public models, 10 design partners, with 2 people) is not credible; realistic is llm-compressor + llama.cpp adapters + gate + card. Labs shipping native low-precision checkpoints (Gemma 4 QAT, Kimi K3 MXFP4, DeepSeek-V4 FP4+FP8, NVIDIA NVFP4 builds of Qwen3.6/Kimi-K2.6) shrink 'build a quant' to 'eval someone else's quant'; `quantc eval` is the right answer but it is a $9 re-eval, not a business. Revenue is Nota/Pruna-shaped (per-build $29-599, Team $399/mo, $150-250k ARR year 1; Nota listed with ~$5.9M revenue, Pruna ~$2.8M); Indian buyers pay for GPUs not tools, so US customers via HF/OSS are needed from day one. The recipe-corpus flywheel needs ~1,000 builds before `plan` beats hand-stitched ModelOpt, and quantcard-as-standard needs OpenRouter/HF/Ollama adoption a 2-person Bengaluru team cannot force. Net: the right machinery, the wrong moat; loses by one point on exactly the two criteria this review exists to judge.
- **vertical (Sankshep)** (30): The only design whose quantization work yields an asset open source cannot replicate: an Indic, 8 kHz, code-mixed, entity-labelled calibration and eval corpus (IndicCalib-v1 / BharatVoiceEval) and recipes gated per language rather than on an English average (MILU per-language recovery >=98.5%, slot/entity F1 drop <=0.5, script-integrity <=0.1% which is the documented non-Latin failure mode), plus a falsifiable, unstudied hypothesis (H1: Indic-matched calibration recovers at least half of the 3.8-4.7-pt INT4 tax from EMNLP 2025) with a 256->4,096-sample sweep that ScaleQ-1.58 suggests matters. The 24 GB-card arithmetic is correct and is the real wedge: Llama-3.1-8B at 128 KiB/token FP16 KV gives ~60 concurrent 2k-token calls at FP16 KV vs ~120 at FP8 KV on an L4, Gemma's head_dim 256 doubles KV and needs the sliding-window skip, W4A16 24B leaves ~55 calls; component choices are right (CTranslate2 int8_float16 for Whisper, sherpa-onnx int8 conformer with hallucination guards, Kokoro ONNX int8, LMDeploy INT8 KV on Ampere restricted to head_dim-128 models, n-gram speculation on W4A16 targets, no EAGLE on INT4 per SpecMQuant, sub-4-bit and sub-8-bit KV explicitly not shipped). Harsh parts: the binding constraint is base-model ASR on telephony audio (IndicWhisper still 26.8% WER on GramVaani), a fine-tuning problem, so quantization is the enabling constraint rather than the whole product; if H1 fails the LLM answer is INT8/FP8 on L4, which is one llm-compressor line, and the moat collapses to data + telephony + compliance. The surface (ASR+LLM+TTS+Pipecat telephony+diarization+PII redaction+QA rubric+Helm+air-gap+outsourced annotation) is too wide for two people; Mode B will be a demo video, which the plan admits. Several load-bearing facts are marked '(verify)' (Sarvam API prices, DPDP dates, Parler/Voxtral licenses; IndicF5 has no license at all). GTM risk is real: Skit/Gnani are full-stack competitors not obvious buyers, bank cycles run 6-12 months, and Sarvam (4,096 subsidised H100s, Apache-2.0 models) could bundle on-prem voice. Capital is modest (Rs 7-11 lakh for 8 weeks, Rs 1-1.3 Cr/yr) and pilots are paid (Rs 3-5 lakh) with per-customer value tooling cannot reach (Rs 6-8 lakh/node/yr; a 200-channel deployment saves Rs 40-85 lakh/month vs cloud APIs). Timing is specific and fresh (RBI FREE-AI Aug 2025, DPDP Rules Nov 2025, Sarvam/IndicConformer open releases, L4 at Rs 49/hr). Wins by a single point, inside judgment noise, on differentiation, defensibility and timing; loses to quantc on feasibility and capital efficiency, which the grafts below are meant to fix.
- **edge (Fewbit)** (25): Quantization policy is the most evidence-consistent in the set for small models: imatrix-calibrated Q4_K_M default with Unsloth-style per-tensor overrides, Q8_0 KV only (no Q4 KV on <=4B given TurboQuant's 1-4-pt losses at 4-bit), ternary only for natively trained BitNet/Falcon-E, and a QAD tier (torchao QATConfig / llm-compressor QADModifier, 1-5k steps, Rs 2-8k of H100) as the actual lever where PTQ fails (INT4 ~94% on a 1.5B reasoning model, AQLM 2-bit Llama-3.2-1B MMLU 0.455->0.289, Gemma 3 QAT cut Q4_0 degradation 54%). Per-SoC sustained-load/thermal/RSS certification and the device x model x quant corpus are things Arm and Qualcomm do not publish. But the product is four SDKs (Kotlin/JNI, Swift xcframework, C++, Python), six runtimes/targets (llama.cpp+KleidiAI, ExecuTorch XNNPACK 8da4w and QNN 16a4w, MLX, ORT GenAI/Olive, bitnet.cpp), resumable signed OTA, telemetry, dashboard and Helm, in 8 weeks with a founder plus one mobile hire; the design itself says that without that hire it is 'a CLI and a hub'. QNN is a swamp (77-minute Qwen3-0.6B conversion, GenieX still developer preview with Gemma-4 E4B accuracy issues, Ollama/LM Studio ignoring NPUs). The India mass-market thesis fails on its own numbers: 5-8 tok/s on Dimensity 7xxx, 2-5 tok/s on 4 GB phones with thermal throttling, plus 1.5-2.5 GB downloads over mobile data, so it becomes flagship-only, i.e. the users cloud already serves well. Pricing at $0.005/MAD is at parity with cloud ($0.006/user/month at 100k tokens on Simplismart's Gemma-3-1B), so the CFO pitch only works for heavy voice use. It is squeezed between free generic paths (Apple Foundation Models, Gemini Nano/AICore, Phi Silica, Gemma 4 QAT with day-0 llama.cpp/MLX/LiteRT) and funded peers (Ollama $65M and 8.9M devs, NimbleEdge in Bengaluru, Cactus, Nexa, Picovoice), with Qualcomm now owning Edge Impulse and Modular. Moat is honestly zero at month 8; OTA lock-in and telemetry network effects exist only once a fleet exists. Its own stated outcome is a $5-50M acquisition.
- **serving (Nibble)** (23): The most engine-literate serving policies of the four: FP8 KV only when served context >=4k (vLLM break-even ~7k tokens), --kv-cache-dtype-skip-layers sliding_window for Gemma/gpt-oss, calibrated KV for MLA models, sequential non-tree drafting on W4A16 targets per SpecMQuant, EAGLE-3 trees only on FP8/INT8 targets, auto-disable speculation below 1.15x at the endpoint's median batch, NVFP4 withheld for 7-14B because 95-98% recovery fails the GOLD gate. None of it is proprietary: it is vLLM 0.20 with correct flags plus llm-compressor recipes, and the design concedes Simplismart or Baseten can copy the card and precision pin 'in one sprint'. Marketing creeps in: '~800 tok/s saturated capacity' on an L40S is quoted alongside EAGLE-3, which yields ~1.16x at batch 32 and adds draft overhead at saturation; Red Hat's 830 figure is INT8 W8A8 with no speculation. Unit economics are a GPU-resale business: L40S at $1.95 managed vs $1.20 raw is ~$540/month gross per endpoint at 35-45% margin, Indian ACVs are $1-5k/month, and the design itself needs 60-100 endpoints for ~$1M ARR, so it is sales-bound, while serverless floors ($0.02-0.14/M for 8B) cap the upside and any customer that grows past ~2,000 tok/s churns upward to H100 FP8 at Fireworks or Simplismart. Operationally a solo founder cannot carry a 99.5% SLA (stated in the design); it needs an SRE by month 2-3, SOC 2 ($20-30k), committed capacity (Rs 20-40 lakh) before 99.9%, and E2E/Neysa L40S inventory is thin while Yotta is aligned with Simplismart. The accuracy-floor SLA invites disputes (200-item eval stderr is 2-3 pts against a 1.5-pt threshold). Sub-8-bit KV is correctly banned, which means >=128k agent workloads stay on H100/H200 with incumbents. The precision ledger, the card-only SKU and India price points are the only durable assets; the rest is a thinner Simplismart with no kernels, no NVIDIA relationship and no US revenue.

Ideas worth grafting:
- From quantc: replace sankshep.lock with quantc's versioned hardware capability DB + pinned 'toolchain' releases + nightly drift rebuilds (format x engine version x SM generation x kernel, weekly-verified), and make `sankshep plan` read it, so the Ampere/Turing/Ada/CPU recipe tiers are machine-checked rather than hand-maintained.
- From quantc: adopt the quantcard JSON schema verbatim as the Eval Card (per-task score vs BF16 with std-error and paired bootstrap, mean/99.9pct KL, CoT-length ratio, tool-call accuracy, GuideLLM perf, Rs per 1M tokens / per call-minute, cosign signature) and ship the GitHub Action gate plus `eval` on third-party artifacts (Sarvam, Unsloth, RedHatAI, Google QAT) as the free top-of-funnel that feeds the Indic Quant Index.
- From quantc: automate the week-2 mixed-precision hypotheses with the per-block KL sensitivity scan -> OR-Tools ILP assignment under a bits-per-weight budget, with hard rules (embeddings/lm_head >=8-bit for 262k-vocab Gemma and Sarvam's expanded tokenizer, first/last blocks one step higher, routers/shared experts >=8-bit, ViT untouched) and a promote-on-failure loop with max_iters, instead of hand-testing layer variants.
- From quantc: the 'quantization audit + recipe' fixed-fee engagement (Rs 3-5 lakh per model x hardware pair) that leaves the customer a repo-committed recipe and card is a cleaner bridge revenue than Sankshep's broader pilots; run it for Indic ISVs bringing their own fine-tunes before any Mode B work.
- From quantc: the Sarvam partnership pitch (official INT4/FP8/GGUF builds of Sarvam 30B/105B with per-language recovery cards) and the E2E/Jarvislabs/Neysa 'certified catalog' channel for their L4/L40S/A100 fleets, which gives Sankshep distribution that does not depend on bank sales cycles.
- From Nibble: the card-only SKU ($299 standard suites / $999 with customer eval, or Rs 25-80k) as a self-serve tier under Sankshep's Rs 1.5-3 lakh certification service, converting readers of the Indic INT4-tax post who will never deploy the stack.
- From Nibble: x-precision / x-recipe / x-card response headers plus the precision-pin and accuracy-floor contract terms (no recipe change without a new card and explicit promotion; automatic rollback to the next-higher precision; credits capped at monthly fees and limited to precision drift) so the Eval Card becomes an enforceable clause in bank vendor agreements rather than a PDF.
- From Nibble: the weekly drift monitor (500 Presidio-scrubbed production prompts replayed on a 1-hour spot H100 BF16 shadow, ~$4/week/model, KL and task-proxy recomputed, card 'last verified' updated) so Eval Cards stay live through engine upgrades, and the 48-hour ledger cadence for every notable Indic/open model release with submission to Artificial Analysis.
- From Nibble: encode its spec-decode and KV rules in `sankshep plan` (FP8 KV only when context >=4k, auto-disable speculation when measured speedup <1.15x at the endpoint's median batch, sequential drafting on W4A16 targets, EAGLE-3 only on FP8/INT8 at batch <=8, calibrated KV for MLA models) and its SKU table discipline (do not list T4 unless the gate passes on it).
- From Fewbit: add the QAD tier (torchao QATConfig / llm-compressor QADModifier, 1-5k steps, Rs 2-8k of H100 per model) for the <=4B CPU and branch-office tier where PTQ fails the Indic gate, exported to Q4_0 GGUF and 8da4w; this is the only credible path to W4 on small Indic models.
- From Fewbit: the automated per-device perf gate (sustained 5-minute decode, peak RSS, thermal throttle <60% of peak, TTFT at 2048 tokens) and the published 'Can I run it?' matrix, applied per exact GPU/CPU SKU and driver, to replace Sankshep's estimated concurrency-per-node table with measured, certified numbers.
- From Fewbit: adapter-only updates (base artifact shipped once, 20-80 MB LoRA adapters served via vLLM multi-LoRA or llama.cpp runtime adapters) for air-gapped refreshes, and the optional hybrid fallback to any OpenAI-compatible cloud endpoint (including Simplismart) when a node is saturated, which positions Sankshep as complementary rather than competitive.

### Judge 3 — winner: Sankshep (vertical)

- **quantc (devtool)** (30): Most buildable of the four: pure Python over llm-compressor/lm-eval/GuideLLM, no SDKs, no on-call, ~$3-4k of rented GPU for 8 weeks. But the buyer is the weakest. A 1-5 person platform team is asked to pay $399/month or $29-599 per build for a wrapper over tools NVIDIA (ModelOpt AutoQuantize + KV AutoQuant in 0.46-0.49), Red Hat (HIGGS and AutoRound AutoScheme inside llm-compressor) and Intel (INC autotune with tolerable_loss) give away, and the digest's own comps say compression tooling monetises badly: Nota ~$5.9M revenue at a $462M IPO, Pruna ~$2.8M, TheStage/Ora/SqueezeBits at seed scale. Of the 'first 10 calls' only 3-4 are plausible payers (a voice-agent company, a DPDP fintech, maybe Sarvam); E2E/Jarvislabs/Inferless want a free catalog, Ollama/OpenRouter/Unsloth/Nexa are partnerships, and the design itself concedes Indian customers pay for GPUs not tooling and that it needs US customers from day one with no US entity. Technical differentiation is real but thin: sensitivity scan + ILP is what AutoQuantize/AutoScheme already do; what is new is multi-backend neutrality, the quantcard, pinned toolchains and the 'eval someone else's quant' wedge (well timed given Gemma 4 QAT and official NVFP4 builds). Incumbent response is the killer: Simplismart adds an 'auto-quantize with eval' button (the design admits one sprint), NVIDIA/Red Hat ship a free gate CLI, and the quantcard 'standard' only works if OpenRouter/HF adopt it, which a 2-person Bengaluru team cannot force. Burn is excellent ($300-400k to month 12) but the stated 12-month outcome is $150-250k ARR funded by ₹3-5 lakh services engagements, i.e. a tool business with an acqui-hire exit.
- **Fewbit (edge)** (26): Two people shipping Kotlin + Swift + C++/JNI + Python SDKs, ExecuTorch QNN exports (77-minute conversions, GenieX still 'developer preview' with Gemma-4 E4B accuracy issues), MLX, Olive/ONNX, a control plane with OTA and telemetry, and a device rack in 8 weeks is three startups; the design says outright that if the mobile hire fails 'the product is a CLI'. Market timing gets the harshest score: the priority segment (6 GB Dimensity/Snapdragon 6-series budget phones, ARPU in tens of rupees) delivers 3-8 tok/s with thermal throttling and needs 1.5-2.5 GB downloads over Indian mobile data, and the design's own price check shows per-device pricing ($0.005/MAD) is at parity with cloud tokens ($0.006/user/month on Simplismart's Gemma-3-1B), so the pitch is privacy/offline, not cost, to a budget owner (Head of Mobile at a low-ARPU app, or Micromax/Lava on razor-thin hardware margins) who is not a software buyer. Platform vendors give the generic path away (Apple Foundation Models, Gemini Nano/AICore, Phi Silica, Gemma 4 QAT at 1 GB), Qualcomm bought Edge Impulse and Modular, and funded direct competitors exist (Ollama $65M/8.9M devs, NimbleEdge in Bengaluru, Cactus, Nexa on Hexagon). The first-10 list is mostly partners (Sarvam, Brave/Proton/Obsidian), grant-funded NGOs, OEMs, and automotive with multi-year cycles; Jio builds in-house. Credit for the per-SoC certification + 'Can I run it?' corpus, QAD tier and adapter-only OTA, which nobody publishes; defensibility via telemetry network effects and release-loop lock-in is real but 'zero at month 8' by their own admission. ₹1-1.2 Cr for 12 months is lean, but an 18-month target of $300-600k ARR behind a 2,000-MAD free tier that captures most of the developer value is a weak return.
- **Nibble (serving)** (27): Strongest buyer story of the four: an existing GPU bill ($2k-60k/month on dedicated H100s at 10-30% utilisation) and the anchor 'cut it 40-70% or pay nothing'; the L40S FP8 math (Red Hat's 830 out tok/s on Llama-3.1-8B INT8 at $1.20/hr raw vs Simplismart H100 FP16 at $4/hr) is credible, and precision pin + accuracy floor in an SLA is a term no vendor offers. Everything else is weaker. It runs head-on into Simplismart's self-declared niche ('best for inference in your own cloud or data center, BYOC, air-gapped'); Simplismart already lists L4 at $1.50 and A10G at $2.00, earns margin on throughput rather than markup, and can match Nibble's $0.95/$1.60 overnight, while Inferless, Turiyam and Pipeshift x Neysa already occupy the Indian dedicated/sovereign lane. The design concedes the planner, gateway, Helm chart and card are copyable in a sprint, and there are zero custom kernels: the only technical asset is the ledger. A solo founder cannot honour even 99.5% uptime (admitted), free 2-week pilots on rented GPUs burn cash, and air-gapped, Whisper, Blackwell and AMD are all post-MVP. Capital efficiency suffers from the business model: the managed tier is GPU resale at 35-45% gross margin, needs ₹20-40 lakh of committed capacity by ~20 endpoints, Indian mid-market ACVs of $1-5k/month mean 60-100 endpoints for $1M ARR, and the month-12 target of $100-120k MRR is a sales-headcount problem the plan does not fund. Fireworks and NVIDIA are irrelevant here; Simplismart is the entire competitive risk, and it is better capitalised (58 people, NVIDIA, Yotta channel, AWS/Azure Marketplace).
- **Sankshep (vertical)** (32): Wins on buyer and incumbent response, not on engineering. Buyer with budget: BPOs and collections teams where cost per call-minute is the P&L (human agent ₹3-5/min, Western voice stacks ₹7-8/min, Indian cloud APIs ₹1.5-3/min, pay-off only below ~₹0.5/min), voice ISVs/CCaaS (Exotel, Ozonetel, Skit, Gnani) with BFSI contracts now forced into VPC/on-prem, and a CISO/model-risk reviewer who needs a per-language Eval Card under RBI FREE-AI/DPDP. Pricing is in the buyer's own units (₹/channel, ₹/audio-minute, ₹/node) and pilots are paid (₹3-5 lakh), not free. The first-10 list is the most concrete of the four, every name has a specific reason and an existing budget line, and Mode A (batch call QA overnight on T4/CPU) is a low-risk entry that avoids live-call liability. Incumbent response: Simplismart (US-majority revenue, InVideo/HeyGen/Higgsfield video customers, H100-first, FP16 default, no FP8 on Ampere) will not go down-market to ₹0.30/min Indic telephony on T4/L4; Fireworks and NVIDIA are irrelevant. The real threats are Sarvam (Apache-2.0 models, 4,096 H100s, enterprise on-prem) and call-QA incumbents the design does not name (Convin, Observe.AI) that Mode A competes with. Technical differentiation is the most specific of the four: whole-path quantization (CTranslate2/ONNX int8 ASR, FP8/INT8/W4A16 LLM, FP8/INT8 KV, int8 TTS), an Indic calibration corpus testing a published and unaddressed -3.8 to -4.7 pt INT4 tax, script-integrity and entity-error gates, and the 24 GB-card KV math (60 to 120 concurrent calls at FP8 KV) are not in any vendor toolkit. Defensibility: BharatVoiceEval telephony sets, auditor-accepted Eval Cards and CCaaS adapter lock-in are the best compounding assets a 2-person team can build, though Sarvam could copy them in a quarter once shown. Feasibility 5 is the honest penalty: ASR + LLM + TTS + telephony + QA + Helm/air-gap in 8 weeks with two people, a binding constraint (IndicWhisper 26.8% WER on GramVaani) that quantization does not fix and needs fine-tuning, and a dozen '(verify)' numbers. ₹7-11 lakh to MVP, ₹1-1.3 Cr for 12 months, paid pilots from month 2-3 and ₹2-3 Cr ARR by month 18 is small but real, with a profitable-niche or Indian-cloud/CCaaS/Sarvam acquisition path.

Ideas worth grafting:
- From Nibble: make the Eval Card a contract term, not a PDF: precision pin (served recipe hash cannot change without a new card and explicit customer promotion), accuracy floor with GOLD/SILVER grades, credits (capped at monthly fees, precision-drift only) and automatic rollback to the next-higher precision for 30 days; add x-precision / x-recipe / x-card headers on every API response.
- From Nibble (plus Fewbit for air-gapped sites): weekly drift check that replays 500 Presidio-scrubbed sampled production turns on a 1-hour spot H100 BF16 shadow (KL + task proxy, ~$4/week/model) and updates the card's 'last verified' block; where prompts cannot leave the perimeter, use Fewbit's on-node canary set (20 fixed prompts scored locally) so regressions show up as a graph rather than a compliance incident.
- From Nibble: the public ledger as the content engine: FP8/INT8/W4A16 Eval Cards for every Sarvam, Gemma, IndicConformer and Whisper release within 48 hours, reproducible GuideLLM configs contrasted with Simplismart's single-user H100 peaks, and submission of hosted models to Artificial Analysis; plus a Card-only SKU (₹25-80k / $299-999 per model x recipe x hardware) for ISVs who will not run Sankshep but need the audit artifact.
- From Nibble: the pricing anchor 'we cut your GPU/API bill 40-70% or you pay nothing' and a BYOC per-GPU-hour software fee (~$0.25/GPU-hr plus a platform minimum) for customers already on AWS Mumbai / GCP asia-south1 VPCs, which widens the segment beyond 'must be on-prem' (the design's own risk that many banks accept Mumbai VPCs).
- From quantc: turn sankshep.lock into a published pinned toolchain image (toolchain:2026.10) with a nightly rebuild of the top recipes against the next vLLM/llm-compressor/compressed-tensors candidate and alerts on load failures or recovery drops, sold as the churn-absorption line inside the per-node licence.
- From quantc: a versioned hardware capability DB behind sankshep plan that states the unpleasant truths (no FP8 on A100/A10G, NVFP4 memory-only on Hopper, W4A16 no throughput gain over FP8 at high concurrency, T4 has no Marlin, head_dim-256 Gemma FP8-KV TTFT penalty) and a ₹/call-minute and ₹/M-token calculator across E2E, Jarvislabs, AWS ap-south and IndiaAI-subsidised (₹67-92/hr) rates.
- From quantc: publish the Eval Card as an open, machine-readable JSON schema (model hash, recipe, calibration hash, toolchain, per-task and per-language recovery with stderr, KL, launch flags, cosign signature), render it as a Hugging Face model-card section and badge, and pitch it to OpenRouter/Ollama-style catalogs as the precision label, so Sankshep is the issuer of a disclosure format rather than only an Indic-voice vendor.
- From quantc: the free 'audit any artifact' wedge: sankshep gate run on Sarvam, Unsloth, RedHatAI, NVIDIA and Google QAT checkpoints, packaged as a GitHub Action ('Indic Quant CI'), feeding the Indic Quant Index leaderboard as the SEO/Show HN asset and the top of the funnel for the certification service.
- From Fewbit: a QAD tier (torchao QATConfig or llm-compressor QADModifier, 1-5k steps, 6-20 H100-hours, ₹2-8k of compute per 1-4B model; Gemma 3 cut Q4_0 degradation 54% with ~5k steps) as the fallback when hypothesis H1 fails and W4A16 misses the per-language gate for the 24B-on-A10G case; start from vendor QAT checkpoints (Gemma 4 QAT) exported to the matching Q4_0/w4a16 format instead of re-quantizing.
- From Fewbit: signed-manifest OTA with adapter-only updates (20-80 MB LoRA GGUF/compressed-tensors adapters over a once-shipped base), staged rollouts by cohort, rollback by alias and resumable chunk-hashed downloads, reused for Sankshep's quarterly air-gap refresh media and for branch/kiosk CPU nodes.
- From Fewbit: a public, quarterly-refreshed 'calls-per-node' matrix (GPU/CPU SKU x model x precision -> concurrent calls, peak RSS, sustained tok/s, ₹/min) as both the sales table and the deterministic input to sankshep plan, replacing the architecture's estimates with measured cells from week 5 onward.
- From Fewbit: a CPU/Jetson/branch edge tier via a Python SDK that returns a local OpenAI-compatible server (llama-server subprocess with Indic-imatrix GGUF) for agent-assist at bank branches and kiosks, and the explicit 'Sarvam as partner, not customer' framing with co-published Indic eval deltas to defuse the biggest competitive threat.
- From Nibble and quantc: a speculative-decoding canary per endpoint (auto-disable if <1.15x at the observed batch bucket; sequential non-tree drafts only on W4A16 targets per SpecMQuant; acceptance rate logged on the card) and a licence-hygiene bill of materials on every card (exclude GPTQModel's AGPL Swordfish kernel, unlicensed evalchemy and IndicF5) so bank procurement sees an Apache/MIT-only stack.


---

## Design [devtool]: quantc (pronounced "quant-see") — "the quantization compiler". CLI: `quantc`. Working name; alternatives: Bitbudget, Recipe.

**One-liner:** An open-core quantization compiler: point it at any Hugging Face model, a target hardware fleet (A10G/L4/L40S/A100/H100/B200/CPU/phone) and an accuracy budget; it searches quantization recipes (method x precision x per-layer mixed precision x KV-cache) across llm-compressor, AutoRound, ModelOpt and llama.cpp, gates every candidate against your own eval set and a BF16 baseline, and emits a signed, deployable artifact (compressed-tensors for vLLM/SGLang/lmdeploy, ModelOpt checkpoint for TensorRT-LLM, GGUF, ExecuTorch .pte) with a machine-readable "quantcard" of provenance, accuracy deltas and launch flags. Terraform/Vercel for quantized models: you commit a `quantc.yaml`, CI blocks the deploy if recovery drops below budget.

**Target customer:** Primary (first 12 months): the 1-5 person platform/ML-infra team at a Series A-C company that self-hosts open models on vLLM/SGLang/llama.cpp on 4-200 GPUs and is (a) stuck on the Ampere/Ada tier (A10G, A100, L4, L40S, RTX 4090 — the cheapest GPUs on E2E, Jarvislabs, Lambda, AWS g5/g6) where FP8 is unavailable and INT8/INT4 is the only lever, or (b) trying to fit a 27B-120B model on fewer/cheaper GPUs, or (c) shipping GGUF/ExecuTorch builds to CPU/edge. They currently either run BF16 (paying ~2x) or ship an unaudited community quant. Budget authority: $5-50k/yr for tooling, more if it replaces GPUs. Concrete profiles: voice-agent and support-automation companies (Gemma/Qwen 4-12B on A10G/L4 at p95 latency SLOs), Indian GPU clouds that need a quantized model catalog (E2E TIR, Jarvislabs, Neysa, Yotta), serverless-GPU players (Inferless) who need small, fast-loading artifacts, and model labs (Sarvam) that need official INT4/FP8 builds with per-language eval deltas. Secondary (months 9-24): regulated BYOC/on-prem buyers (Indian fintech/health under DPDP, EU banks) who need precision disclosure and an audit trail, bought via an enterprise self-hosted runner. Explicitly NOT the customer: anyone buying tokens from an API (DeepInfra/Groq/Together at $0.05-0.14/M for 8B are unbeatable), and frontier-lab-scale users who have their own quantization teams.

**Problem:** Quantization is now free but unusable as a workflow:

1. Toolkit churn is the pain. AutoAWQ (archived May 2025), AutoGPTQ (archived Apr 2025), optimum-quanto (maintenance) are dead; TorchAO says it is minimizing new features; llm-compressor ships a breaking release every ~6 weeks (0.13 Aug 2026, 0.14 Sep 2026, hotfix Oct 22); TensorRT-LLM 1.2 deleted its whole engine backend. A recipe that worked in Q2 silently fails to load in Q4.
2. Auto-search exists only in vendor silos. ModelOpt AutoQuantize (NVFP4/FP8/BF16 under an effective_bits budget, KV AutoQuant in 0.48/0.49), AutoRound AutoScheme, llm-compressor HIGGS, `mistralrs tune` — none spans vLLM + llama.cpp + ExecuTorch, none knows your fleet, none takes an accuracy budget on YOUR eval set.
3. Hardware support is a minefield. FP8 W8A8 needs SM8.9+ (no FP8 on A100/A10G — Simplismart's own docs say so); NVFP4 is native only on SM100 and runs as Marlin W4A16 on H100 (memory savings, no speedup over FP8); W4A16 gives almost no throughput gain over W8A8 on H100 (Red Hat); consumer Blackwell SM120 NVFP4 GEMMs were producing wrong results (TRT-LLM #14154); Marlin is absent on Volta/AMD/CPU. Engineers learn this by crashing production.
4. Per-model recipes are fragile and nobody records them. AWQ collapsed Qwen2-VL-2B from 67.2 to 7.9 avg while GPTQ held 56.0; gpt-oss FP8 KV must skip sliding-window layers; ModelOpt exported NVFP4 KV scales 6x wrong until 0.49; shared experts in MoEs are disproportionately sensitive; W4 is near-lossless only for >=14B reasoning models and inflates chain-of-thought length on smaller ones.
5. No accuracy gate exists as a product. Practitioners hand-stitch lm-eval-harness + GuideLLM + ad-hoc KL checks. Hosted providers do not even disclose precision (a 2026 audit found only DeepInfra and Baseten label it on OpenRouter; "silent quantization" is now a governance complaint). Red Hat's 500k-eval study shows W4A16 averages 99.4% recovery but worst-task 96.9% — the tail is exactly what a gate must catch, and nobody ships one.

Net effect: teams overpay for BF16 on H100s or ship degraded quants they cannot explain to their customers. Simplismart solves this as bespoke services inside a closed platform (the Sanas Gemma-3 INT4 H100->A10G case). The job to be done — "make this model fit this budget on this hardware without breaking my eval" — has no reproducible, versionable, CI-able tool.

### Product

## What it is
Three layers, open-core:

1. **`quantc` CLI + library (Apache-2.0)** — runs locally on your GPU. Spec in, artifact + quantcard out.
2. **quantc Cloud (SaaS)** — hosted recipe search on rented GPUs (so you do not need an H100/B200 to calibrate FP8/NVFP4), private artifact registry, CI gate, drift alerts, cost dashboard.
3. **Enterprise runner** — the same control plane self-hosted/air-gapped, with support SLA and curated eval packs (Indic, regulated-domain).

## The spec (`quantc.yaml`)
```yaml
model: Qwen/Qwen3-8B                       # any HF repo or local path; LoRA merge optional
targets:
  - name: prod-l40s
    hardware: nvidia/l40s                    # a10g, l4, a100-80g, h100, h200, b200, rtx4090, rtx5090, cpu/x86-amx, apple/m4, android/sd8e-gen5
    engine: vllm>=0.20
    workload: {input_tokens: 4000, output_tokens: 400, concurrency: 16, p95_ttft_ms: 800}
  - name: laptop
    hardware: cpu/x86-avx512
    engine: llama.cpp
budget:
  accuracy:
    suites: [gsm8k_cot, ifeval, mmlu_pro_1k, humaneval_plus]   # standard, versioned
    custom: ./evals/support_tickets.jsonl                      # your prompts + graded answers / judge rubric
    tools: ./evals/tool_schemas.json                           # function-call accuracy gate
    min_recovery_avg: 0.99                                     # vs BF16 run on the same engine
    min_recovery_per_task: 0.97
    max_mean_kl: 0.02                                          # logits vs BF16 on 1k held-out prompts
  bits: {max_effective_weight_bits: 4.5, kv: auto}
calibration:
  samples: 512
  seq_len: 2048
  sources: [./data/prompts.jsonl, self_generated_cot]          # mixes your traffic + model's own reasoning traces
search: {max_iters: 4, methods: [fp8, int8_smoothquant, gptq, awq, autoround, nvfp4]}
```

## Commands (UX)
- `quantc plan` — no GPU needed. Reads the hardware capability DB + recipe corpus and prints candidate recipes with predicted memory, tok/s, $/M tokens and expected recovery, and tells you the unpleasant truths ("INT4 will not speed up H100 at concurrency 32; use FP8", "A10G has no FP8; best is INT8 W8A8 + W4A16 fallback", "NVFP4 on H100 is memory-only").
- `quantc build [--remote]` — runs the search (local GPU or quantc Cloud), produces `out/<target>/` with weights, `quantcard.json`, `serve.sh` (exact vLLM/SGLang/llama.cpp flags, e.g. `--kv-cache-dtype fp8 --kv-cache-dtype-skip-layers sliding_window`), and a Dockerfile.
- `quantc eval <artifact>` — re-runs all gates on any artifact (ours, RedHatAI's, Unsloth's, NVIDIA's) and emits a card. This is also the free "audit any quant" wedge.
- `quantc diff a b` — side-by-side cards (precision per layer, recovery per task, $/M).
- `quantc push oci://registry/org/model:tag | hf://org/model` — artifact + card + signature (cosign) to any OCI registry or HF Hub.
- `quantc serve <artifact>` — launches the engine with the recorded flags; smoke-tests generation.
- `quantc toolchain pin 2026.10` — a tested, pinned set of (torch, vLLM, llm-compressor, compressed-tensors, ModelOpt, llama.cpp commit) versions; Cloud rebuilds your top recipes nightly against the next toolchain and alerts on breakage.
- GitHub Action `quantc/gate@v1` — fails the PR if a model/recipe change drops below budget.

## The quantcard (the thing nobody ships)
`quantcard.json`: model + revision hash; recipe (method, per-layer scheme, group size, KV scheme, ignore list, transforms); calibration set hash + composition; toolchain versions; engine + kernel used (e.g. `marlin_w4a16`, `cutlass_fp8`); hardware compat matrix (native / fallback / unsupported per SM gen); eval table per task with BF16 baseline, quantized score, recovery, std-error, n; mean/99.9pct KL; CoT-length ratio; tool-call accuracy; perf (TTFT/ITL/throughput at the declared workload); $/M tokens on 3 clouds; launch flags; signature. Rendered as a model-card section on HF and as a badge.

## API surface
- Python: `quantc.plan(spec) -> Plan`, `quantc.build(spec, remote=False) -> Artifact`, `quantc.evaluate(artifact, budget) -> Card`, `Artifact.serve_cmd(engine)`.
- REST (Cloud): `POST /v1/builds`, `GET /v1/builds/{id}` (streams logs), `GET /v1/artifacts`, `GET /v1/cards/{id}`, `POST /v1/evals`, webhooks on build/drift events; OCI distribution API for pull.
- Web: build history, cards, cost dashboard (tok/s and $/M per SKU per artifact), drift alerts.

## What it is NOT
No serving, no GPU ownership, no autoscaling, no fine-tuning UI, no diffusion/video in v1, no NPU in v1. The artifact runs on any engine, any cloud — including Simplismart's, Baseten's, or your own K8s. (The "leaner" reading of "quantized Simplismart" is exactly this: one job, text LLM/VLM, zero ops surface.)

### Technical architecture

## Components
1. **`quantc-core`** (Python 3.11, Typer + Pydantic)
   - *Spec parser* and *hardware capability DB* (versioned JSON, the heart of `plan`): per target -> SM/arch, VRAM, bandwidth, supported formats and the kernel that will actually run, plus a $/hr table (E2E, Jarvislabs, AWS ap-south, GCP, Lambda, RunPod). Seed table:
     | target | SM | FP8 W8A8 | INT8 W8A8 | W4A16 | NVFP4 | FP8 KV |
     |---|---|---|---|---|---|---|
     | T4 | 7.5 | no | no | yes (non-Marlin GPTQ/AWQ kernels) | no | no |
     | A10G / A100 | 8.6 / 8.0 | **no** | yes (SmoothQuant+GPTQ) | yes (Marlin) | weight-only fallback | no calibrated scales (llm-compressor needs CC>8.9) |
     | L4 / L40S / RTX 4090 | 8.9 | yes | yes | yes | fallback | yes |
     | H100 / H200 | 9.0 | yes | yes | yes (no speedup vs FP8) | Marlin fallback, memory only | yes |
     | B200 / GB200 | 10.0 | yes | yes | yes | **native** | yes + NVFP4 KV |
     | RTX 5090 / RTX PRO | 12.0 | yes | yes | yes | flagged *unstable* (TRT-LLM #14154, llama.cpp PR #26704 open) | yes |
     | x86 CPU (AMX/AVX512) | - | - | INT8 (AMX) | GGUF Q4_K/Q5_K/Q6_K via llama.cpp | - | GGUF q8_0 KV |
     | Arm (Axion/Graviton/Android) | - | - | INT8 | GGUF Q4_0 + KleidiAI / ExecuTorch 8da4w | - | int8 KV (ExecuTorch Arm) |
   - *Backend adapters* (one class each, all behind a `Quantizer` interface): `llmcompressor` (GPTQ, AWQ, SmoothQuant, AutoRound modifier, FP8/NVFP4/MXFP4, FP8/NVFP4 KV, HIGGS) -> compressed-tensors; `modelopt` (NVFP4/FP8/INT4-AWQ, AutoQuantize) -> HF checkpoint for TRT-LLM 1.x PyTorch backend and vLLM; `llamacpp` (`llama-imatrix` on our calibration set -> `llama-quantize --imatrix` with per-tensor overrides) -> GGUF; `executorch` (torchao `Int8DynamicActivationInt4WeightConfig` / SpinQuant + XNNPACK, QNN 16a4w) -> .pte (phase 2); `hqq` as the fast calibration-free proxy for sensitivity scans.
   - *Planner/searcher* (below).
   - *Eval runner*: lm-evaluation-harness 0.4.13 with vLLM/SGLang/llama.cpp backends, custom-task YAML generated from the customer's JSONL (exact-match, regex, or LLM-judge via any OpenAI-compatible endpoint), KL/logit diff harness, long-context NIAH/RULER slice, tool-call checker, CoT-length monitor. BF16 baseline is cached per (model revision, engine version, task version).
   - *Perf runner*: GuideLLM (sweep/constant/poisson) against the engine launched with the artifact; converts to $/M tokens with the price table and the declared SLO.
   - *Packer*: writes `quantcard.json`, `serve.sh`, Dockerfile; pushes via ORAS to OCI or `huggingface_hub`; signs with cosign.

2. **Control plane (quantc Cloud)**: FastAPI + Postgres + Redis (RQ) + S3/R2; GPU workers = pinned "toolchain" containers launched on RunPod/Modal (global) and E2E/Jarvislabs (India) by job class: L40S for <=14B INT8/FP8, H100 for 27-120B, B200 by the hour for NVFP4 native calibration/perf. Streams logs via SSE; Stripe + Razorpay billing; Grafana/Loki for ops. Registry = OCI (any registry works: GHCR, ECR, Harbor) so enterprises can self-host with zero new infra.

3. **Recipe corpus**: Postgres table of (arch family, size, MoE/VLM flags, target, recipe, eval deltas, toolchain) seeded from our own public builds and, opt-in, anonymized customer builds. `plan` queries it as the prior; it is the data flywheel.

## Search algorithm (what "compiler" means)
- **A. Prior**: nearest recipes from corpus for (arch family, params, target). If a stored recipe meets budget on the standard suite, skip to D with it.
- **B. Sensitivity scan**: BF16 forward over 128 calibration samples, cache block outputs. For each transformer block (and separately attention vs MLP, and expert groups for MoE), quantize with HQQ/RTN at each candidate precision (W8, W4-g128, W3, FP8, NVFP4) and measure KL divergence of final logits vs BF16 (not per-block MSE; perplexity is explicitly not used, it understates activation-quant damage). Cost for an 8B model: ~32 blocks x 3 precisions x 128 samples = a few minutes on an L40S.
- **C. Assignment**: OR-Tools ILP: minimize sum of sensitivities s.t. weighted average bits <= `max_effective_weight_bits`, with hard rules: lm_head/embeddings >= 8-bit, MoE routers and shared experts >= 8-bit, ViT untouched for VLMs, first/last block one step higher, Hopper never assigned a format that has no speedup at the declared concurrency.
- **D. Real quantization** with the chosen method (GPTQ for dense W4, AWQ when GPTQ fails the VLM/text check, SmoothQuant+GPTQ for INT8 W8A8, AutoRound for <=3-bit or mixed-bit, FP8/NVFP4 via llm-compressor or ModelOpt) on 512 x 2048 chat-templated samples (20 for NVFP4 per llm-compressor guidance), `add_special_tokens=False`, evaluated with `add_bos_token=True`.
- **E. Gates** in the real target engine (load + generate smoke test first; this alone catches most format bugs). On failure: promote the top-k most sensitive layers one precision up, or switch method, up to `max_iters`. If still failing: emit the best card and a clear "budget not achievable on this hardware" verdict with the next-cheapest hardware that would.
- **F. Perf** at the declared workload; **G. Pack + sign**.

## Data flow
`quantc.yaml` -> plan (CPU, seconds) -> build job (GPU, 20 min for 8B W4A16 on L40S; ~2-4 h for 70B incl. evals on H100) -> gates -> perf -> artifact + card -> registry -> `serve.sh` / CI.

## Stack (pinned in toolchain 2026.10)
PyTorch 2.11, transformers, llm-compressor 0.14.x, compressed-tensors, auto-round, nvidia-modelopt 0.46-0.49, vLLM 0.20+, SGLang (eval backend), llama.cpp (pinned commit), ExecuTorch 1.5 (phase 2), lm-eval 0.4.13, GuideLLM, OR-Tools, HQQ; FastAPI, Postgres, Redis, S3/R2, ORAS, cosign, Docker. All Apache-2.0/MIT/BSD; GPTQModel's AGPL Swordfish kernel is deliberately excluded.

## Hardware the team needs
No owned GPUs. Dev: one L40S on E2E ($1.20/hr) most days; H100 ($3.99/hr) for 27-70B runs; B200 ($7.99/hr) a few hours a week for NVFP4; A100-80GB ($2.10) and an A10G (AWS g5) to validate Ampere paths; a Snapdragon phone and an M-series Mac for phase-2 edge targets.

### Quantization strategy

## Default recipe ladder per target (what `plan` proposes first)
- **B200/GB200**: FP8 W8A8 + FP8 KV as the lossless default; NVFP4 weights (+ FP8 attention) for >=27B where the gate allows (Red Hat data: ~99% recovery at 70-235B, 95-98% at 7-14B — so 8B models stay FP8 unless the customer eval passes); NVFP4 KV only with calibrated scales and a long-context gate.
- **H100/H200**: FP8 W8A8 + FP8 KV. W4A16 only when the goal is fit (e.g. 70B on one GPU), with the card stating "no throughput gain over FP8 at this concurrency". No NVFP4 (memory-only fallback) unless fit demands it.
- **L4/L40S/RTX 4090 (Ada)**: FP8 W8A8 + FP8 KV first; INT8 W8A8 (SmoothQuant+GPTQ) as the alternative (Red Hat: Llama-3.1-8B 14.9->8.0 GB, 576->830 tok/s on L40S); W4A16 GPTQ-g128 for fit (27B on a 48 GB L40S).
- **A10G/A100 (Ampere) — the wedge Simplismart does not emphasise**: INT8 W8A8 (SmoothQuant+GPTQ) for throughput; W4A16 GPTQ/AWQ via Marlin for fit (Gemma-3-12B/Qwen3-14B on a 24 GB A10G); KV stays BF16 or uses lmdeploy's online INT8 KV where head_dim=128.
- **T4**: W4A16 only, non-Marlin kernels; plan warns about speed.
- **x86 CPU**: GGUF Q4_K_M / Q5_K_M / Q6_K with imatrix on the customer calibration set; INT8 for AMX boxes (INT4 is cast to INT8 on AMX anyway); ternary only for natively trained BitNet/ParetoQ models via bitnet.cpp.
- **Arm/Android/iOS (phase 2)**: ExecuTorch 8da4w (W4 group-wise, 8-bit dynamic activations) + SpinQuant rotations; GGUF Q4_0 + KleidiAI as the fallback; QNN 16a4w for Hexagon.
- **MoE (gpt-oss, Qwen3-A3B, DeepSeek, Kimi)**: experts to NVFP4/MXFP4/W4, attention + shared experts + router FP8/BF16, per-expert scales (ModelOpt 0.47+ format), REAP expert pruning offered as an explicit, separately gated option.
- **VLM**: quantize the language tower only by default (Qwen3-VL practice); ViT stays BF16; AWQ is disallowed for VLMs unless it passes a VLM gate (the Qwen2-VL collapse).
- **Reasoning/RL-tuned models**: W4 only for >=14B; W8/FP8 below; KV >= FP8; calibration must include self-generated CoT traces; a CoT-length gate is mandatory.

## Methods we use and why
GPTQ and AWQ (tied at 4-bit; both via llm-compressor), SmoothQuant+GPTQ for INT8 W8A8, AutoRound (SignRoundV2) for 2-3-bit and mixed-bit, QuaRot/SpinQuant rotations for W4A4/edge, HQQ only as a proxy in sensitivity scans, FP8/NVFP4/MXFP4 via llm-compressor or ModelOpt, imatrix for GGUF. Not in v1: vector quant (AQLM/QTIP/VPTQ — no production kernels upstream), 3-bit KV (TurboQuant 3-bit loses ~20 pts on reasoning per vLLM's study), W4A4 on Hopper (no kernels). QAT/QAD (llm-compressor QADModifier, torchao QATConfig, Gemma-3-style ~5k steps) is phase 2, offered when PTQ cannot meet budget on a <=12B model.

## Guardrails (all must pass; all are in the card)
1. **Load + generate smoke test** in the exact target engine version.
2. **Recovery**: avg >= 0.99 and per-task >= 0.97 (defaults; customer-settable) vs a BF16 baseline run on the same engine, same seeds, with std-error; a paired bootstrap flags deltas within noise instead of failing them.
3. **Logit fidelity**: mean KL <= 0.02, 99.9th pct < 0.5 on 1k held-out prompts from the customer's own traffic (Unsloth-style KLD; catches damage perplexity hides).
4. **Structured output / tool calls**: JSON validity and function-call accuracy on the customer's tool schemas (FP4 errors concentrate on low-entropy tokens like digits and operators).
5. **Reasoning**: on GSM8K-CoT/MATH-500/AIME subsets, score recovery AND mean output tokens <= 1.10x BF16 (token inflation check).
6. **Long context**: if `input_tokens` > 8k, NIAH/RULER slice at 32k/64k/128k with per-head calibrated FP8 KV scales when uncalibrated recovery < 95%; sliding-window layers skipped automatically.
7. **Multilingual**: if >10% of customer prompts are non-English (detected), per-language sub-gate using the customer set plus IndicGenBench/MMLU-style slices (INT4 hurts low-resource languages 3.8-4.7 pts more; we gate per language rather than on the English average).
8. **Perf**: TTFT/ITL/throughput at the declared workload must meet the SLO, else the card says so and `plan` proposes the next recipe or hardware.
9. **Reproducibility**: calibration-set hash, seeds and toolchain pinned; `quantc eval` reproduces the card to within std-error or the build is flagged.

## Evaluation suites (versioned, shipped with the toolchain)
Standard: MMLU-Pro (1k stratified), GSM8K-CoT, IFEval, HumanEval+, TruthfulQA (the historical worst case), ARC-C; add-ons: MATH-500/AIME24 (reasoning), RULER (long context), BFCL-style tool calling, MMMU slice (VLM), IndicGenBench/Flores slices (multilingual). Custom sets are first-class and recommended; the card distinguishes public-benchmark recovery from private-eval recovery so contamination does not fake a pass.

## Honest limits
- Calibration for FP8/NVFP4 activation quant needs SM8.9+/SM100 GPUs; hosted search exists precisely so Ampere-only customers can get FP8 artifacts for their newer nodes.
- We cannot make INT4 fast on H100 or FP4 fast on Hopper; the planner says so instead of pretending.
- 3-bit and ternary PTQ of instruct models will mostly fail the gate; we say "QAT or a natively trained model" rather than ship it.

### Differentiation vs Simplismart

**Simplismart** is a closed, proprietary serving platform (engine + Terraform-like orchestration, 58 people, ~$21M raised, NVIDIA as investor/partner) that sells GPU-hours ($1.20-$5.20/hr) and tokens ($0.13/M for Llama-3.1-8B) and earns its margin from throughput-per-GPU. Quantization there is a configuration knob (FP16/BF16/FP8/AWQ/GPTQ) plus bespoke services (the Sanas Gemma-3 INT4 H100->A10G job). Public gaps: FP8 unsupported on Ampere, nothing on NVFP4/MXFP4, QAT, sub-8-bit KV, automatic accuracy-guarded search, no edge/CPU/on-device, no precision disclosure, zero open-source and therefore zero community pull, and no neutral benchmark audit.

**quantc** differs on every axis that matters:
1. **Layer, not platform.** We sit upstream of every engine — vLLM, SGLang, lmdeploy, TensorRT-LLM, llama.cpp, ExecuTorch — and of every host, including Simplismart, Baseten, Together or the customer's own K8s. We own no GPUs and sell no tokens, so we are complementary to serving clouds (even a potential channel for them) rather than a price competitor in a market with a $0.05-0.14/M floor.
2. **Accuracy budget is the product.** Simplismart optimizes speed/cost and delivers accuracy anecdotally ("99.99% task accuracy"). We make the accuracy gate, the eval card, the per-layer precision map and the reproducibility hash the deliverable. Nobody — not Simplismart, Together, Fireworks, Baseten — ships a signed precision disclosure today.
3. **Cheap and awkward hardware is the wedge.** Simplismart's cheapest tier (T4/L4/A10G/A100) is exactly where it has no FP8 and only AWQ. Our planner is built around Ampere/Ada INT8/INT4, CPU GGUF and (phase 2) phones/NPUs — markets Simplismart does not serve at all.
4. **Open-core vs closed.** The CLI, adapters, hardware DB and eval gates are Apache-2.0, like llm-compressor/Pruna/Unsloth; we monetize hosting, registry, CI and enterprise runners. This gives community distribution Simplismart structurally cannot get.
5. **Churn absorption.** Pinned toolchains and nightly drift rebuilds are a product feature; Simplismart absorbs churn only inside its own engine.
6. **Pricing model.** Per build / per seat / per enterprise runner (tool budget) instead of per GPU-hour (infra budget) — a different buyer line item and no infra margin risk.
7. **Scope ("quantized" in the lean sense).** One job, text LLM/VLM only, no orchestration, no fine-tuning UI, no autoscaling — shippable by 2-3 people, whereas Simplismart needs 58.

What we do NOT beat them on, and should not try: raw serving throughput (28 custom kernels, Eagle-3, Dynamo integration), enterprise BYOC/air-gapped ops, GPU procurement, sales team, NVIDIA relationship. If a customer wants a managed endpoint, we hand them an artifact and point them to any host.

### Moat

Be honest first: the algorithms (GPTQ/AWQ/FP8/NVFP4/AutoRound) are commoditized and owned by Red Hat, NVIDIA and Intel; kernels are owned by vLLM/NVIDIA/llama.cpp. A moat here is workflow, data and trust, built over 12-24 months, and it is modest:

1. **Recipe corpus flywheel.** Every build (ours public, customers' opt-in anonymized) adds (arch, size, target, recipe, per-task deltas, toolchain) rows. After ~1,000 builds, `plan` predicts a passing recipe before any GPU runs, cutting search cost and time below what a user stitching ModelOpt or llm-compressor by hand can match. This corpus does not exist anywhere public today (HF Hub is a blob store; RedHatAI/NVIDIA cards are not machine-readable across formats).
2. **Compatibility matrix as a maintained asset.** Weekly-verified "format x engine version x SM generation x kernel" table and pinned toolchains. Toolkit churn (AutoAWQ/AutoGPTQ deaths, TorchAO wind-down, TRT-LLM 1.2 backend removal, SM120 bugs) is a recurring pain that compounds in our favor as long as we keep paying the maintenance cost.
3. **quantcard as a disclosure standard.** If OpenRouter-style audits, Ollama's library, Indian GPU clouds' catalogs or a regulator reference it, the card becomes the neutral precision label and we are the issuer. This is the only path to a real network effect; it is also the hardest.
4. **CI lock-in.** Once `quantc.yaml`, eval sets and thresholds live in a customer's repo and their deploy pipeline blocks on our gate, switching cost is real even though the tool is open-source (Terraform's lesson).
5. **Private eval sets + regulated runners.** Enterprise customers' calibration/eval data stays in their runner; the relationship is the moat, not the code.
6. **Multi-vendor neutrality.** NVIDIA's AutoQuantize will never optimize for AMD MXFP4, Intel AMX, Arm or Qualcomm; Red Hat's will stay vLLM-centric. Being the neutral layer across NVIDIA/AMD/Intel/Arm/Apple/Qualcomm is defensible exactly because each vendor is structurally unable to do it.

Expected end state: the historical pattern is that independent optimization layers get acquired by chip vendors or platforms within 2-3 years (Deci, OctoAI, Neural Magic, SqueezeBits, Modular, Edge Impulse). A tool with a recipe corpus, a disclosure standard and 50-100 paying teams is an attractive target for AMD, Qualcomm, Arm, a GPU cloud (E2E/Yotta/Nebius), Ollama or a serving cloud; that is a legitimate outcome for a capital-light founder, not a failure.

### 8-week MVP

Assumes 2 engineers (founder + one backend/infra engineer), ~$4-6k of rented GPU time, nothing owned. Everything below is scoped to text LLMs on NVIDIA GPUs + CPU GGUF; VLM/MoE handling is best-effort; no edge, no QAT, no diffusion.

**Week 1 — skeleton and first real artifact**
- Repo `quantc` (Apache-2.0), Typer CLI, Pydantic spec, hardware capability DB v0 (T4/A10G/A100/L4/L40S/4090/H100/B200/x86 CPU) with E2E/AWS/RunPod prices.
- llm-compressor adapter: W4A16 (GPTQ), W8A8-INT8 (SmoothQuant+GPTQ), FP8 W8A8, FP8 KV scheme -> compressed-tensors; load+generate smoke test in vLLM.
- Run on Llama-3.1-8B-Instruct and Qwen3-8B on a rented L40S. Deliverable: `quantc build` produces a vLLM-loadable artifact.

**Week 2 — the gate**
- lm-eval-harness wrapper (vLLM backend), BF16 baseline caching keyed by (model rev, engine, task version), standard suite v0 (MMLU-Pro-1k, GSM8K-CoT, IFEval, HumanEval+, TruthfulQA), std-error and paired comparison.
- KL/logit-fidelity harness on held-out prompts; custom JSONL task compiler (exact/regex/judge).
- `quantcard.json` v0 + `serve.sh` emission. Deliverable: build fails/passes against `min_recovery`.

**Week 3 — the compiler**
- Sensitivity scan (HQQ/RTN per block x {W8, W4, FP8}, KL on logits), OR-Tools assignment under `max_effective_weight_bits`, hard rules (lm_head/embeddings/router/shared experts), mixed-precision export through compressed-tensors `config_groups`.
- Iterative promote-on-failure loop (`max_iters`).
- GuideLLM perf run at the declared workload; $/M-tokens calculator. Deliverable: `quantc plan` with predictions and `quantc build` that searches.

**Week 4 — second target + go public**
- llama.cpp adapter: imatrix from the same calibration set -> `llama-quantize` Q4_K_M/Q5_K_M/Q6_K with per-tensor overrides; llama.cpp eval backend for the gate.
- Docker toolchain image `quantc/toolchain:2026.10` with pinned versions.
- Publish repo + HF org with 12 quantized models (Llama-3.1-8B, Qwen3-4B/8B/14B, Gemma-3-4B/12B/27B, Mistral-Small, Phi-4, gpt-oss-20b, Qwen3-30B-A3B, DeepSeek-R1-Distill-14B) each with a card, on L40S/A10G/A100 targets. Blog: "12 models, 3 cheap GPUs, 99% recovery: every recipe and every failure".

**Week 5 — hosted search**
- FastAPI control plane, Postgres, Redis/RQ, S3/R2; worker launcher on RunPod/Modal (global) and E2E (India); `quantc build --remote` with SSE logs; GitHub OAuth; Stripe + Razorpay metered billing per build.
- Private registry: OCI push/pull via ORAS (works against GHCR/ECR/Harbor), HF Hub push, cosign signatures. Deliverable: a stranger can run a 70B FP8 build without owning an H100.

**Week 6 — CI and drift**
- GitHub Action `quantc/gate@v1` (fails PR below budget, posts the card diff as a comment).
- Nightly drift job: rebuild top-20 corpus recipes on the next toolchain candidate; alert on load failures or recovery drops.
- ModelOpt adapter for NVFP4 (calibrate on B200 by the hour; export vLLM/TRT-LLM-PyTorch checkpoint); planner marks NVFP4 memory-only on Hopper.

**Week 7 — design partners and the sharp edges**
- Run 10 design-partner builds on their models and eval sets (target: 5 Indian, 5 global; see GTM). Add what they break: reasoning gate (CoT length, MATH-500 slice), tool-call gate, VLM text-only quantization, MoE rules, sliding-window KV skip, head_dim != 128 handling.
- Seed the recipe corpus with ~40 public builds; `plan` uses it as prior.

**Week 8 — launch and harden**
- Resumable builds, calibration caching, cost guardrails on hosted jobs, docs site, pricing page.
- Show HN + vLLM/SGLang community posts + Bengaluru ML meetup talk; HF org at 25 models; three short case studies from design partners (e.g. "Gemma-3-12B voicebot from H100 to L4 at 99.2% recovery, 61% lower $/M tokens").
- Success metric for week 8: 300 GitHub stars, 20 hosted builds by non-partners, 3 signed Team pilots or 1 paid audit engagement (₹3-5 lakh).

**Cut from the 8 weeks on purpose:** QAT/QAD, ExecuTorch/QNN, Apple MLX, diffusion/video, SGLang-specific exports, TurboQuant/4-bit KV, Indic eval packs (added in weeks 9-12 with a partner lab), enterprise self-hosted runner (month 4-6).

### GTM

## Motion: bottom-up open source + 10 hand-picked design partners + services to seed revenue

**Channels**
- HF Hub org with quantcard-bearing models (the way RedHatAI, Unsloth and NVIDIA distribute); every card links back to the recipe.
- Monthly "Quantization on cheap GPUs" report: neutral, reproducible numbers for A10G/L4/L40S/A100 across engines (the digest found zero neutral audits in this space — we become the audit).
- vLLM/SGLang/llama.cpp communities (docs PRs, Discord), GitHub Actions marketplace, PyTorch/vLLM meetups, Bengaluru ML meetups.
- Partnerships with Indian GPU clouds (E2E TIR, Jarvislabs, Neysa, Yotta) for "quantc-certified" catalogs — they want more tokens per rupee on the Ampere/Ada fleets they already own.
- Precision-label partnerships: OpenRouter, Ollama library, DeepInfra.

**Pricing**
- **OSS (free, Apache-2.0)**: CLI, all adapters, hardware DB, local builds and gates, cards.
- **Cloud builds (metered)**: priced per build, cost-plus on rented GPUs: $29 for <=10B, $149 for <=80B, $599 for <=500B (search + full gate + perf); re-evals $9. (Cost basis: 8B W4A16+eval ~90 L40S-minutes ~ $2-3 of GPU; 70B FP8 ~3 H100-hours ~ $12-15.)
- **Team $399/month**: 10 builds included, private registry (50 artifacts), CI gate, drift alerts, cost dashboard, email support.
- **Enterprise $36k-$90k/year**: self-hosted/air-gapped runner, SSO, audit export, Indic/regulated eval packs, custom calibration-set construction, named support with 2-business-day fixes for toolchain breakage, optional accuracy-SLA addendum (we commit to re-search until recovery >= X or refund the build).
- **Services (months 1-6, honest bridge)**: "Quantization audit + recipe" fixed-fee engagements at ₹3-5 lakh ($4-6k) per model/hardware pair — the same bespoke work Simplismart did for Sanas, but it leaves the customer with a repo-committed `quantc.yaml` and a card. Target: 6 engagements in the first 6 months = ~$30k, enough to fund GPUs.

**Revenue goal**: 12 months: ~$150-250k ARR (25 Team, 2 Enterprise, services); 24 months: $1M ARR requires ~10 Enterprise runners — that is the test of whether this is a venture business or a nice tool business (Nota AI at IPO: ~$5.9M revenue; Pruna ~$2.8M).

**First 10 customers/partners to call (with the specific pitch)**
1. **E2E Networks (TIR)** — quantized, carded model catalog for their A100/L40S/L4 fleet; co-marketed "more tokens per rupee".
2. **Jarvislabs** — same for their templates; they already publish India H100 price benchmarks.
3. **Inferless** (Bengaluru, serverless GPU) — INT8/W4 artifacts cut cold-start and let them sell cheaper SKUs.
4. **Sarvam AI** — official INT4/FP8/GGUF builds of Sarvam-30B/105B with per-language recovery cards (nobody has published Indic-calibrated quant recipes; they have 4,096 H100s and an Apache-2.0 release to protect).
5. **Sanas AI or a comparable voice-agent company (e.g. Ozonetel, Skit.ai, Gnani)** — Gemma/Qwen 4-12B on A10G/L4 at p95 TTFT SLOs; this is exactly the Simplismart bespoke case, productized.
6. **Pipeshift x Neysa** (sovereign inference stack) — they need reproducible quantized stacks with disclosure for government/regulated buyers.
7. **Ollama** — audited GGUFs with cards for the library; they have 8.9M monthly devs and just raised $65M for hybrid cloud.
8. **OpenRouter** — a precision label standard (quantcard badge) solves their "silent quantization" complaints with providers.
9. **A fintech document-extraction team under DPDP (Signzy, Perfios or Setu)** — on-prem SLM at W8/W4 with an auditable card; first Enterprise runner.
10. **Nexa AI** (NPU) or **Unsloth** — partnership, not customer: ExecuTorch/QNN export in phase 2 with Nexa; Unsloth Dynamic GGUF cards via `quantc eval` (co-marketing, zero cost).

**Positioning line**: "Quantization you can put in CI and show your customers."

### Team and cost

**Team (months 0-6)**
- Founder-engineer (you): quantization, engines, planner, evals; owns the HF org and blog. Must be able to read llm-compressor/vLLM source and debug kernels-by-version, not just call APIs.
- Engineer 2 (hire by week 3, ₹2.5-4 lakh/month or equity-heavy): control plane, workers, registry, billing, CI action, drift system — a strong Python/FastAPI/Kubernetes-lite generalist.
- Optional person 3 (month 4+): DevRel/eval engineer producing the monthly cheap-GPU report, Indic eval packs and design-partner onboarding; can be a contractor or a strong intern from IIT/IISc.
Advisors worth one call each: someone from the vLLM/llm-compressor community, someone who has sold tooling to Indian GPU clouds.

**Cost, first 8 weeks**
- GPU rental: L40S $1.20/hr x ~300 h = $360; H100 $3.99/hr x ~150 h = $600; B200 $7.99/hr x ~40 h = $320; A100-80GB $2.10/hr x ~100 h = $210; A10G (AWS g5) ~$100; hosted-job buffer for design partners ~$1,500. Total ~$3-4k (₹2.5-3.5 lakh).
- Infra: Postgres/Redis/S3-R2/domain/CI ~ $150/month; Modal/RunPod minimums ~$100/month.
- People: 2 engineers x 2 months at India senior rates ≈ ₹10-16 lakh ($12-19k) if paid; near zero if founder-only + equity.
- 8-week total: ~₹13-20 lakh ($15-25k) cash, or ~$5k if the founder works unpaid.

**Runway to a fundable milestone (12 months)**
- 3 people, GPU spend scaling to ~$2-3k/month as hosted builds grow (mostly pass-through), infra $500/month, misc/legal/travel ~$10k: ~₹2.5-3.5 Cr ($300-400k) all-in. That is a pre-seed/angel round (Titan Capital, Antler, Better Capital, iSeed, Peak XV Surge are the natural names) — far below Pruna's $6.5M or TheStage's $4.5M seeds, which is the point: capital-light until the corpus and the card standard prove out.
- Break-even test at month 12: ~$20k MRR covers 3 salaries + GPUs at Indian cost structure.

**What the money does NOT buy**: no owned GPUs, no sales team, no kernels of our own. If the business needs those, it has become Simplismart and should not be built by 2 people.

### Why now

1. **The tooling just consolidated, so a compiler can finally target a stable set of backends.** AutoAWQ (May 2025) and AutoGPTQ (Apr 2025) are dead, quanto is in maintenance, TorchAO is winding down features; what remains is llm-compressor (now vLLM's official quantization library, with AutoRound merged in Dec 2025), NVIDIA ModelOpt, Intel AutoRound and llama.cpp. Four adapters cover ~95% of production paths for the first time.
2. **The decision space exploded past human search.** In 18 months the menu went from 'FP16 or AWQ' to FP8/INT8/W4A16/NVFP4/MXFP4/MXFP6, FP8 vs 4-bit vs TurboQuant KV (vLLM backend merged Apr-May 2026), per-layer mixed precision, per-expert scales, rotations, and per-SM-generation kernel availability. A 70B MoE on a mixed A100/L40S/H100 fleet has thousands of valid recipes; vendor auto-tools search only their own corner.
3. **Hardware fragmentation makes hardware-aware selection valuable.** Hopper has no FP4; Ampere has no FP8; W4A16 does not speed up H100; SM120 NVFP4 is buggy; AMD has native MXFP4/MXFP6; Intel AMX is INT8-only; TPU Ironwood just got native FP8. The right recipe now depends on the exact SKU, and fleets are heterogeneous.
4. **Disclosure is becoming a demand, not a nicety.** 'Silent quantization' is a 2026 governance complaint; audits show only DeepInfra and Baseten label precision on OpenRouter; enterprise contracts cover uptime but not FP16-vs-FP8; EU/India regulated deployments want an audit trail. No vendor sells a signed precision card.
5. **Reasoning and agentic models created new failure modes** (CoT token inflation, digit/operator errors at FP4, KV error accumulation, calibration-data sensitivity) that the 2024-era 'perplexity looks fine' check misses — a reason the gate has to be rebuilt now.
6. **The cheap-GPU tier is where India's compute is.** India has ~34k GPUs heading to 100k by Dec 2026, mostly A100/L40S/L4-class on E2E, Yotta, Neysa and IndiaAI Mission subsidised nodes (₹67-92/hr); INT8/INT4 on Ampere/Ada is the economic lever there, and Simplismart's own docs say it has no FP8 on that tier.
7. **Category validation with the thesis left open.** Simplismart's $14M Series B (today, NVIDIA participating, 'fewer GPUs' pitch), Multiverse's $570M at $1.7B, PrismML's Khosla seed, Ollama's $65M, Inferact's $150M seed and DeepInfra's $107M prove buyers pay for efficiency and that distribution partners exist — while every one of them treats quantization as a feature or a black box rather than a reproducible, accuracy-guarded artifact pipeline.
8. **Labs now ship QAT (Gemma 3/4) and native FP4 models**, which means the next wave of demand is not 'quantize Llama' but 'verify, re-target and re-gate someone else's low-precision checkpoint on my hardware and my evals' — exactly what `quantc eval` and the card do.

### Risks

- Vendor pre-emption: NVIDIA ModelOpt AutoQuantize (per-layer NVFP4/FP8/BF16 under effective_bits, KV AutoQuant in 0.48/0.49) and Red Hat's llm-compressor HIGGS/AutoRound AutoScheme already do the search inside their silos; a free 'quantize with gate' CLI from either erases the OSS layer. Mitigation is multi-vendor neutrality and the card/registry/CI layer, which is a thinner moat than kernels.
- Compression-tool revenue is historically small: Nota AI listed on KOSDAQ with ~$5.9M revenue, Pruna ~$2.8M, TheStage/Ora/SqueezeBits at seed scale; most outcomes were acqui-hires by chip vendors. The realistic ceiling may be a $1-5M ARR tool business or an acquisition, not a $100M company.
- Toolkit churn can break us as fast as it breaks customers: llm-compressor releases every ~6 weeks, TensorRT-LLM removed its engine backend in 1.2, TorchAO is winding down features, ModelOpt changed MoE checkpoint formats in 0.47; maintaining 4-5 adapters plus a weekly-verified compat matrix is a permanent 0.5-1 FTE tax for a 2-3 person team.
- Labs ship native low-precision checkpoints (Gemma 4 QAT for every size, Kimi K3 MXFP4 QAT, DeepSeek-V4 FP4+FP8, gpt-oss MXFP4, NVIDIA NVFP4 builds of Qwen3.6/Kimi-K2.6/DeepSeek-V3.2), shrinking PTQ demand for the most popular models to 'eval the official quant' rather than 'build one'.
- Hardware economics undercut the pitch on high-end GPUs: W4A16 gives little throughput gain over W8A8 on H100 and NVFP4 is memory-only on Hopper, so the value concentrates on Ampere/Ada and fit cases; if customers migrate to B200 and native NVFP4, our wedge narrows to edge/CPU.
- Accuracy gates can be gamed or misread: public benchmarks are contaminated, customers may not have graded eval sets, and a '99% recovery' card can be mistaken for a contractual guarantee; an accuracy-SLA addendum creates liability a small company cannot carry, and a single public failure (a reasoning model inflating CoT or a tool-call regression) damages the trust that is the whole product.
- Reasoning/agentic models degrade in ways the field has not solved (token inflation, low-entropy-token errors, KV error accumulation over long traces, calibration needing millions of reasoning tokens); if our gates reject most sub-8-bit recipes for these models, the product looks useless on the models customers care about most in 2026.
- Hosted search has thin unit economics for large models: a 400B+ build needs multi-GPU calibration and hours of H100/B200 time; per-build pricing may not cover failed searches, and spot availability on E2E/RunPod is unreliable.
- India go-to-market risk: Indian customers historically pay for GPUs, not tooling; Simplismart itself gets >50% of revenue from the US; we may need US customers from day one, which a Bengaluru-based 2-person team without a US entity reaches only via open source and HF.
- Simplismart, Baseten, Together or Fireworks can add an 'auto-quantize with eval' button inside their platforms; we only survive that if the artifact portability and disclosure card are things customers demand of their host rather than from us.
- Consumer Blackwell (SM120) and NPU paths are immature (TRT-LLM nvfp4_gemm correctness bugs, llama.cpp SM120 PR unmerged, Qualcomm GenieX still developer preview); promising edge targets in year one risks shipping artifacts that are slower than BF16 or wrong.
- Key-person and burnout risk: the founder is simultaneously the quantization expert, planner author and community face; losing 6 weeks to a kernel bug or illness stalls everything. Glassdoor-style leadership complaints at Simplismart are a reminder that intense small infra teams break.
- License hygiene: GPTQModel's Swordfish kernel is AGPL (excluded on purpose), evalchemy has no license, some Unsloth tooling is AGPL; an accidental dependency could poison the Apache-2.0 story enterprises require.
- Pre-empted 'standard': if OpenRouter, Hugging Face or Red Hat define a precision-disclosure schema first, our quantcard becomes an implementation of someone else's standard, removing the network-effect path.


---

## Design [edge]: Fewbit

**One-liner:** Fewbit is the Expo/Firebase for on-device LLMs: an open-source SDK, a hub of accuracy-certified 4-bit/ternary small models (1-8B), and a fleet/OTA control plane, so apps on phones, laptops, kiosks, robots and CPU-only servers run private, offline, zero-per-token AI that is proven not to have gotten dumber when it got smaller.

**Target customer:** Primary buyer: the Head of Mobile / Platform Engineering at a company that must ship an LLM feature that works offline, keeps data on the device, or has to be free at the margin because the user base is huge and low-ARPU. Champion: the one engineer who already tried llama.cpp on an Android phone, got 4 tok/s and a thermal shutdown, and has no idea whether the Q4 model is still correct in Hindi.

Concrete segments, in priority order:
1. Indian vernacular consumer apps and budget-phone OEMs (6-8 GB RAM Android, Dimensity 6xxx/7xxx and Snapdragon 6/7-series): voice/text assistants, on-device transcription + summarisation, form filling. Zero per-token cost matters because ARPU is tens of rupees.
2. Field-force / health / agri apps (ASHA-worker, CHW, agronomy, insurance-claims apps) where connectivity is intermittent and the data is sensitive.
3. Kiosk, POS and in-vehicle makers (banking/railway kiosks, retail POS, two-wheeler and car infotainment) that ship a fixed SoC and need a model that is certified for that exact board.
4. Robotics and drone companies on NVIDIA Jetson Orin/Thor (VLM for perception + instruction following, air-gapped).
5. Regulated enterprises (banks, hospitals, law firms) deploying assistants on CPU-only laptops (Snapdragon X, Intel/AMD NPUs, Apple Silicon) or on-prem CPU servers under DPDP/HIPAA-style rules.

Explicitly not the target: anyone whose workload is fine on a $0.06-0.13/M-token cloud API, anyone needing >8B models, and anyone who wants us to be their GPU cloud. Geography hypothesis: start India (density of budget Android, DPDP, OEM relationships), sell globally through the open-source SDK.

**Problem:** **The workload is real, the tooling is a swamp.** Running a 1-4B model on a device is now technically possible everywhere (llama.cpp on 132k stars, ExecuTorch 1.5 in production at Meta, MLX, ORT GenAI, Qualcomm Genie), but an app team that wants to ship one has to answer five questions by hand, and each answer is wrong for someone else's phone:

1. **Which quantization is actually safe?** INT4 is ~99% recovery for >=7B (Red Hat/IST Austria, 500k evals) but the numbers get bad exactly where edge lives: INT4 recovers only ~94% on a 1.5B reasoning model, SpinQuant Llama-3.2-1B loses 2 MMLU points, 2-bit collapses small models (Llama-3.2-1B MMLU 0.455 -> 0.289), AWQ on Qwen2-VL-2B collapsed 67.2 -> 7.9 while GPTQ held 56.0, and low-resource languages lose more than English (AWQ-int4 -4.7% on Hindi/Tamil-class languages vs smaller English drops; a 2026 preprint calls it the "multilingual quantization tax"). Nobody ships a gate that says "this Q4 build of *your* fine-tune is within 1% of BF16 on *your* eval, in Hindi, at the context length *this phone* can afford".
2. **Which format for which chip?** The same model needs GGUF (CPU/Metal/CUDA via llama.cpp), .pte with 8da4w (XNNPACK) or 16a4w (Qualcomm NPU) for ExecuTorch, 4-bit MLX for Mac, INT4 ONNX for Windows NPUs, and I2_S for bitnet.cpp. Each has different kernels, different accuracy, and different failure modes (KV quant breaks when head_dim != 128 in LMDeploy; QNN w4a16 conversion of Qwen3-0.6B took 77 minutes; GenieX is still "developer preview" with known accuracy issues on Gemma-4 E4B; Ollama/LM Studio do not use NPUs at all).
3. **Will it run on the user's phone?** India's median Android has 6 GB RAM, a MediaTek or Snapdragon 6/7-series SoC, and throttles after 90 seconds. A 3B Q4 model that does 32 tok/s on a Snapdragon 8 Elite Gen 5 does 5-8 tok/s on a Dimensity 7050 and gets OOM-killed on a 4 GB phone. There is no "Can I run it?" table, so teams either ship only to flagships or ship a broken experience.
4. **How do you update it?** A model is a 0.8-2.5 GB blob. Every app that ships one re-invents download-with-resume, signature verification, staged rollout, rollback and per-SoC variant selection. Nobody ships LoRA-adapter-only OTA even though llama.cpp supports runtime GGUF adapters.
5. **What is it doing in the field?** No tok/s, TTFT, thermal, crash or quality telemetry per SoC/variant. Teams find out from Play Store reviews.

Meanwhile the platform vendors give away *generic* on-device models (Apple Foundation Models ~3B, Gemini Nano via ML Kit/AICore, Phi Silica on Copilot+ PCs, Gemma 4 QAT). They solve none of the above for a company with its own fine-tuned model, its own language mix, its own eval, and a fleet that spans Android + iOS + a kiosk + a Jetson. That workflow gap, not the kernels, is the product.

Secondary reading of the user's question ("a more quantized version of Simplismart" = a leaner company) also holds: this is deliberately one modality class (text/VLM 1-8B), four runtimes, no custom kernels, no GPU cloud.

### Product

## What Fewbit is

Three pieces, one workflow. The developer brings a model (public or their own fine-tune) and an eval set; Fewbit turns it into certified per-target artifacts, serves them to devices, and reports back.

### 1. `fewbit` CLI + Python library (Apache-2.0)
Wraps the maintained OSS quantizers and exporters behind one recipe file and one accuracy gate.

```yaml
# fewbit.yaml
model: google/gemma-4-e4b-it            # or ./my-finetune (safetensors) [+ lora: ./adapter]
targets:
  - android-cpu        # llama.cpp GGUF, KleidiAI arm64
  - android-qnn        # ExecuTorch 16a4w .pte, Snapdragon 8 Gen 3+ NPU
  - ios                # llama.cpp Metal GGUF (xcframework)
  - macos-mlx          # MLX 4-bit
  - jetson             # llama.cpp CUDA GGUF
  - linux-cpu          # llama.cpp AVX512/AMX or bitnet.cpp
budget: { min_ram_gb: 6, max_download_mb: 2600 }
calibration: { customer_prompts: ./prompts.jsonl, languages: [en, hi, ta], tokens: 2_000_000 }
gate:
  kld_mean_max: 0.02
  recovery_min: 0.99          # on customer eval, vs BF16 reference
  general: [ifeval, gsm8k, mmlu_redux_subset]
  indic: [milu_subset, indicgenbench_xlsum]
  tool_calls_json_valid_min: 0.98
  escalate: [Q4_K_M, Q5_K_M, Q6_K, Q8_0]   # auto-raise precision until gate passes
```

```bash
pip install fewbit
fewbit build          # produces artifacts/<target>/<variant>.{gguf,pte,mlx,onnx}
fewbit certify        # runs the gate on cloud + device rack, emits signed eval cards
fewbit publish        # pushes artifacts + cards to registry (private or public hub)
fewbit rollout gemma-4-e4b@3 --cohort 10% --where "soc in (sm8750, sm8650) and ram_gb>=8"
fewbit rollback gemma-4-e4b@3
```

Each build emits an **eval card** (JSON + Markdown): recipe hash, calibration-set hash, quantizer and engine versions, per-task score vs BF16 reference, KL divergence stats (mean, p99), per-language deltas, needle-in-context at 2k/4k/8k, tool-call JSON validity, and per-device perf (tok/s decode, TTFT at 512/2048 prompt, peak RSS, sustained-5-minute throughput, energy per 1k tokens where measurable). Cards are Ed25519-signed; the SDK refuses unsigned artifacts.

### 2. Model Hub (free, public) + private registry
A Hugging Face org (`fewbit/`) plus hub.fewbit.dev with certified builds of the small-model canon: Gemma 4 E2B/E4B (QAT), Qwen3.5 0.8B/1.7B/4B, Llama 3.2 1B/3B, Phi-4-mini, SmolLM3, Sarvam-1 2B and Sarvam 30B-class INT4 for Indic, Qwen3-VL 2B/4B (vision), Whisper small/turbo INT8, BitNet b1.58-2B-4T and Falcon-E ternary. Every entry has: eval card, a **"Can I run it?" matrix** (SoC x RAM x variant -> tok/s / go-no-go), and a download link per target. The hub is content marketing and a trust signal; it is not the business.

### 3. Fewbit Fleet (the paid product)
- **Device SDKs**: Kotlin (Android), Swift (iOS/macOS), C++ (kiosk/embedded/Jetson), Python (robots, servers). One API everywhere, OpenAI-shaped:

```kotlin
val fb = Fewbit.init(context, apiKey = "fb_live_...")
val model = fb.models.resolve("assistant-v3")        // picks best certified variant for THIS device
val chat = model.load()                               // llama.cpp / ExecuTorch under the hood
chat.stream(messages, tools = tools) { token -> ui.append(token) }
```

```python
from fewbit import Fleet
m = Fleet(api_key=...).resolve("jetson-vlm-v2")   # returns a local OpenAI-compatible server
client = openai.OpenAI(base_url=m.base_url)        # drop-in for existing code
```

- **Capability detection**: SoC, RAM, free storage, NPU presence and driver version, OS, thermal headroom -> deterministic manifest resolution against the eval cards (a device only ever receives a variant certified for its class).
- **OTA**: resumable, hash+signature-verified downloads over CDN; staged rollouts by %, app version, SoC, country; instant rollback; **adapter-only updates** (ship the 1.5 GB base once, push 20-80 MB LoRA GGUF adapters for behaviour changes).
- **Telemetry**: load time, decode tok/s, TTFT, peak RSS, thermal state, crashes, context-overflow rate, optional opt-in quality probes (a fixed set of 20 canary prompts scored on-device vs expected outputs) so a regression on a specific SoC shows up as a graph, not a 1-star review.
- **Hybrid fallback** (optional): if a device is below the floor or a prompt exceeds device context, route to any OpenAI-compatible cloud endpoint the customer already has (Simplismart, DeepInfra, their own vLLM). Fewbit does not sell tokens.
- **Dashboard**: fleet by variant/SoC, rollout health, perf percentiles, quality-probe drift, download abandonment.

### Control-plane API (FastAPI, OpenAPI-documented)
`POST /models`, `POST /models/{id}/versions` (artifact + eval card), `GET /resolve?device=...` (manifest), `POST /rollouts`, `POST /rollouts/{id}/rollback`, `POST /telemetry/batch`, `GET /devices`, `GET /cards/{artifact}` (signed card), plus a webhook when a build's gate fails.

### UX principles
Minutes to first on-device token on a real phone (`fewbit demo --android` installs a sample app with a certified Gemma 4 E2B). Nothing closed on the device: the SDK and runtime are Apache-2.0; what you pay for is the registry, OTA, telemetry, and certification of your own models.

### What is weak about this product
It is a workflow and ops layer over other people's quantizers and kernels. If Google/Qualcomm/Apple make the generic path "good enough" and app teams stop fine-tuning, the Hub becomes a nice open-source project and Fleet becomes a feature of Firebase. The defence is being the only thing that works for *custom* models across *mixed* fleets, and being there first with the data.

### Technical architecture

## Components

```
 HF / customer checkpoint (+LoRA, + eval.jsonl, + prompts.jsonl)
          |
   [Build workers]  -- per-target exporters (all OSS, pinned versions)
          |            GGUF: convert_hf_to_gguf -> llama-imatrix -> llama-quantize (+per-tensor overrides)
          |            ExecuTorch: export_llama 8da4w/g128 (XNNPACK), 16a4w (QNN), int8 KV (Arm)
          |            MLX: mlx_lm.convert --quantize --q-bits 4 --q-group-size 64
          |            ONNX: Olive int4 (RTN/AWQ) -> ORT GenAI (CPU/DirectML/QNN/OpenVINO)
          |            Ternary: bitnet.cpp I2_S/TL2 (BitNet/Falcon-E only)
          |            QAT/QAD (tier 2): torchao QATConfig or llm-compressor QADModifier, 1x H100
          v
   [Certify workers] -- accuracy gate (cloud GPU/CPU) + perf gate (device rack / device farm)
          |            lm-eval-harness via llama-server OpenAI backend; llama-perplexity --kl-divergence
          |            customer eval runner (exact/regex/LLM-judge); MILU/IndicGenBench subsets; BFCL-lite
          |            adb/idevice-driven llama-bench + sustained-load + thermal/RSS capture
          v
   [Registry]  Postgres (models, versions, variants, eval cards, rollouts, devices)
               Cloudflare R2 (artifacts; zero egress) + Cloudflare CDN
               Ed25519 signing (keys in control plane; sigstore later)
          v
   [Fleet API]  FastAPI: /resolve (manifest), /rollouts, /telemetry, /devices, webhooks
          v
   [Device SDKs]  fewbit-core (C++ over llama.cpp C API; ExecuTorch runner; MLX via Swift)
                  Kotlin/Swift/Python/C++ wrappers; download manager; signature verify; local
                  OpenAI-compatible server (Python/C++ targets); telemetry batcher
          v
   [Telemetry]  batched JSON -> FastAPI -> Postgres at first, ClickHouse when >50M events/mo
               dashboard: Next.js (or FastAPI+HTMX for v0)
```

## Data flow for one release
1. `fewbit build`: resolves recipe, materialises calibration corpus (customer prompts + general web/chat mix + Indic text in the declared languages + model self-generated completions), runs exporters per target on a build worker. GGUF path runs on CPU or one L4 (Rs 49/hr on E2E); ExecuTorch/MLX/ONNX exports run on CPU; QAT runs on one H100 (Rs 379/hr) for 1-5k steps.
2. `fewbit certify`: accuracy gate first (cheap, cloud), perf gate second (scarce, device rack). The escalation loop re-quantizes at the next precision in the list if the gate fails, and records every attempt in the card.
3. `fewbit publish`: artifacts to R2, card + metadata to Postgres, signature attached.
4. `fewbit rollout`: cohort rules compiled to a manifest resolver; devices poll `/resolve` on app start (and via push for rollback). The resolver is deterministic given (device fingerprint, rollout state) so support can reproduce what a device got.
5. Device SDK downloads (resumable, chunked, hash per chunk), verifies signature, loads into the runtime, emits telemetry.

## Runtime matrix (what runs where, honestly)
| Target | Default runtime | Format | Notes |
|---|---|---|---|
| Android CPU (all SoCs) | llama.cpp, `-DGGML_CPU_KLEIDIAI=ON`, Q4_0 repack for i8mm/SME2 | GGUF | The real mass-market path. 1B at >40 tok/s on S24-class, 5-10 tok/s on Dimensity 7xxx, 2-5 on 4 GB budget phones (measured in week 2, published) |
| Android NPU (Snapdragon 8 Gen 3 / 8 Elite / X) | ExecuTorch QNN 16a4w | .pte | ~32 tok/s for 3B on 8 Elite Gen 5 (Qualcomm figure). Conversion is slow and brittle; certify per SoC, never generic |
| Android GPU (Adreno/Mali) | llama.cpp Vulkan/OpenCL | GGUF | Optional; often loses to CPU on mid-range |
| iOS / iPadOS | llama.cpp Metal (xcframework) | GGUF | ANE is not usable for LLM decode in practice; Apple Foundation Models used as fallback when customer accepts generic model |
| macOS | MLX (preferred) or llama.cpp Metal | MLX 4-bit / GGUF | |
| Windows (Snapdragon X / Intel Core Ultra / AMD) | ORT GenAI via QNN / OpenVINO / DirectML; llama.cpp CPU fallback | ONNX int4 / GGUF | |
| Jetson Orin Nano/NX/AGX, Thor | llama.cpp CUDA (JetPack 6/7) | GGUF Q4_K_M/Q8_0 | vLLM on Jetson only for Thor-class; not in v1 |
| Linux x86 CPU servers | llama.cpp AVX512/AMX (INT8 preferred on AMX); bitnet.cpp for ternary | GGUF / I2_S | |
| Linux Arm servers (Graviton/Axion/Ampere) | llama.cpp + KleidiAI | GGUF | ~50 tok/s 4-bit Llama-class on Axion (Arm figure) |
| Browser | WebLLM/wllama (WebGPU) | MLC / GGUF | Not in v1 |

## Hardware the team owns (one-off, ~Rs 6-7 lakh / ~$7-8k)
Samsung Galaxy S25 (Snapdragon 8 Elite), one 2026 flagship (8 Elite Gen 5), Pixel 9a (Tensor), Redmi/Realme with Dimensity 7050 (6 GB), Snapdragon 6 Gen 1 phone (6 GB), one Rs 8k 4 GB phone, iPhone 16, iPhone SE-class, Mac mini M4 (also the macOS CI runner), Snapdragon X Elite laptop, Intel Core Ultra laptop, Jetson Orin Nano Super dev kit ($249), Raspberry Pi 5 16 GB ($120), one used RTX 4070 desktop for local CUDA. Scale-out via Firebase Test Lab / AWS Device Farm ($0.17/device-minute) for SoC coverage we do not own.

## Stack
Python 3.12, FastAPI, SQLAlchemy + Postgres, Postgres-backed job queue (procrastinate) with worker containers on E2E Networks / Hetzner, Cloudflare R2 + CDN, Ed25519 (PyNaCl), llama.cpp (pinned commit, built with KleidiAI/Metal/CUDA), ExecuTorch 1.5.x, mlx-lm, onnxruntime-genai + Olive, bitnet.cpp, llm-compressor 0.14 + AutoRound (for W4A16 of server-side INT4 and sensitivity scans), torchao 0.18 (QAT), lm-evaluation-harness 0.4.13, custom KLD and device-bench runners, Kotlin + JNI (prebuilt arm64-v8a .so), Swift Package wrapping an xcframework, typer CLI, Next.js dashboard, GitHub Actions + self-hosted mac/Jetson runners.

## Security/compliance basics
Signed manifests and artifacts; model files encrypted at rest on device only when the customer licenses require it (adds load latency, off by default); telemetry contains no prompt text unless the customer opts in a probe set; control plane deployable on-prem (Helm chart) for regulated customers; weight-license checks per model (Gemma/Llama terms) recorded in the card.

### Quantization strategy

## Principles
1. **Memory-bandwidth-bound devices want 4-bit weights; small models want QAT.** On a phone or CPU, decode speed scales with bytes moved, so W4 is the default. But the accuracy evidence is worst for <=4B models at 4-bit, so Fewbit's second tier is quantization-aware training/distillation, not cleverer PTQ.
2. **No FP8/NVFP4 story.** Edge silicon has no FP8/FP4 tensor cores (Apple, Qualcomm, MediaTek, Arm CPUs), Hopper runs NVFP4 as a Marlin fallback, and consumer Blackwell NVFP4 kernels were still broken/slow in llama.cpp and TRT-LLM as of Oct 2026. We only touch FP8 on Jetson Thor-class if a customer demands it.
3. **No proprietary kernels.** llama.cpp k-quants/i-quants, XNNPACK 8da4w, QNN 16a4w, MLX affine 4-bit, ORT int4 and bitnet.cpp I2_S/TL2 are the kernels; Fewbit's work is choosing, calibrating, mixing, gating and shipping.

## Tiers
**Tier 1, PTQ default (every model, every target).**
- GGUF: Q4_K_M as the default; IQ4_XS when the download budget is tight; Q5_K_M/Q6_K/Q8_0 as escalation. Embeddings and output head kept at Q6_K/Q8_0. Always imatrix-calibrated (`llama-imatrix` on the Fewbit calibration corpus, then `llama-quantize --imatrix`), never naive. Per-tensor overrides from a sensitivity scan (below) produce Unsloth-style "dynamic" layouts: first/last blocks and attention projections at 6-8 bit, FFN at 4.
- ExecuTorch: `8da4w` group 128 for XNNPACK (int8 dynamic activations, int4 weights); `16a4w` for QNN; int8 KV cache on Arm.
- MLX: 4-bit, group 64; 8-bit for the output head.
- ONNX/ORT GenAI: int4 (RTN with per-channel scales, AWQ where Olive supports it) for CPU/DirectML/QNN/OpenVINO.
- Server-side INT4 for CPU/Arm servers and Jetson: W4A16 via llm-compressor GPTQ (512 x 2048 chat-templated calibration samples) exported to GGUF or compressed-tensors.
- KV cache: Q8_0 K and V on llama.cpp (near-lossless, halves KV); never Q4 KV on <=4B models (TurboQuant/vLLM data shows 1-4 pt losses at 4-bit and ~20 pt at 3-bit on reasoning; small models are worse). FP8 KV is a server-GPU thing, out of scope.
- Vision-language: quantize the language tower only; keep the ViT at BF16/INT8 (AWQ on Qwen2-VL-2B collapse is the warning).
- Whisper/speech: INT8 (whisper.cpp Q8_0 / Q5_1), not INT4.

**Tier 2, QAT/QAD for custom small models (the paid differentiator).**
- Start from vendor QAT checkpoints when they exist (Gemma 4 QAT E2B/E4B/12B, Llama 3.2 QLoRA/SpinQuant variants). Export those to Q4_0 (the format that matches their fake-quant) and 8da4w.
- For customer fine-tunes: LoRA fine-tune in BF16 -> merge -> QAD with the BF16 fine-tune as teacher (torchao `QATConfig(Int8DynamicActivationInt4WeightConfig(group_size=32), step="prepare"/"convert")` or llm-compressor `QADModifier`), 1-5k steps (Gemma 3 QAT used ~5k steps and cut Q4_0 perplexity degradation by 54%). One H100 for 6-20 hours for a 1-4B model = Rs 2-8k ($25-100) of compute per model. Export to Q4_0 GGUF, 8da4w .pte, MLX 4-bit; re-run the gate.
- Reasoning/thinking small models: default to Q6_K/Q8_0; W4 only after QAD; always include a CoT-length check in the gate ("token inflation" under aggressive PTQ is a 2026 finding).

**Tier 3, ternary / 2-bit for 4 GB phones and tiny CPUs (narrow, honest).**
- Only natively ternary models: BitNet b1.58-2B-4T, Falcon-E, BitNet embeddings, via bitnet.cpp (2.4-6.2x CPU speedup, 0.4 GB non-embedding weights). We do not train ternary models from scratch.
- ParetoQ-style 2-bit/ternary QAT fine-tunes of 0.5-1B models for narrow tasks (classification, intent, slot filling) where a customer eval, not MMLU, is the bar. Never for open-ended generation at <=1B.

## Automatic, accuracy-guarded precision selection (the "auto" in the loop)
1. **Sensitivity scan**: quantize one block/tensor-class at a time at 4-bit (rest BF16), measure KL divergence on 200k calibration tokens; rank; allocate bits greedily under the download/RAM budget. Cheap (<1 GPU-hour on an L4 for a 4B model). Produces the per-tensor override map for llama-quantize and the mixed scheme for AutoRound/llm-compressor where used.
2. **Build the candidate at the lowest precision in the escalation list.**
3. **Gate**, in order of cost: KLD vs BF16 (mean <= 0.02, p99 <= 0.5 by default; these are the ranges Unsloth/bartowski Q4_K_M quants achieve) -> customer eval recovery >= 99% (or their threshold) -> general suite (IFEval, GSM8K-200, MMLU-Redux-500, HellaSwag-500) -> language suite (MILU subset, IndicGenBench XL-Sum/translation chrF for declared languages; token-count sanity for Indic scripts) -> tool-call JSON validity >= 98% on a BFCL-lite set -> needle-in-haystack at 2k/4k/8k -> VLM: TextVQA/DocVQA subset.
4. **Escalate** precision for the failing tensors first (using the scan), then globally; stop at the first passing variant; record every attempt in the card. If even Q8_0 fails the customer eval, the problem is the model, and the card says so.
5. **Perf gate** on real devices: sustained 5-minute decode >= target tok/s, peak RSS <= RAM budget, no thermal throttle below 60% of peak, TTFT at 2048-token prompt <= target. A variant that passes accuracy but fails perf on a SoC class is simply not certified for that class.

## Calibration corpus builder
Customer prompts + general chat/instruction text + Indic text in declared languages + the model's own completions on the customer prompts (self-generated traces reduce distribution mismatch; the reasoning-quant literature shows calibration data lacking the target pattern is the bottleneck). Target 0.5-2M tokens for imatrix, 512 x 2048 samples for GPTQ/AutoRound. Hash stored on the card.

## Known limits we state on every card
Benchmarks are sampled subsets, not full suites; LLM-judge evals use a fixed open judge (Qwen3.5-class) and are noisier than exact-match; language coverage is only what the customer declares; NPU paths are certified per exact SoC + driver version and can regress with OS updates.

### Differentiation vs Simplismart

Simplismart sells *fewer GPUs per workload* in a cloud or customer VPC: closed engine (28 custom CUDA kernels, EAGLE-3, FP8/AWQ), Terraform-like orchestration, per-token ($0.06-0.13/M for 1-8B) or per-GPU-hour ($1.20-5.20), >50% US revenue, video/image-gen-heavy customer list. They have no edge, mobile, NPU or CPU-only-device offering (only a cloud "CPU compute" SKU), no QAT, no public accuracy certification, and nothing open-source.

Fewbit is orthogonal on every axis that matters:
- **Where inference runs**: on hardware the customer's users already own (phones, laptops, kiosks, Jetsons, CPU boxes). Marginal cost per token is zero; Simplismart's is a GPU-hour.
- **Buyer**: Head of Mobile/Platform and product teams shipping app features, not the infra team buying GPU capacity.
- **Unit of value**: per monthly-active device and per certified model, not per token or per GPU.
- **Thesis**: quantization *is* the product (certified 4-bit/ternary builds with signed eval cards and automatic precision escalation). For Simplismart it is one of 140 config options with no accuracy disclosure.
- **Openness**: SDK, CLI and runtime integrations are Apache-2.0; on mobile a closed SDK gets zero adoption, and every runtime we sit on is already open. Simplismart's closed engine is its asset; ours is the workflow and the data.
- **Small models only**: 0.5-8B, where Simplismart's H100 engineering is irrelevant and where accuracy at 4-bit is hardest (so a guardrail is worth paying for).
- **Complementary, not competitive**: Fewbit's hybrid fallback routes overflow to any OpenAI-compatible cloud, including Simplismart. A realistic partnership pitch is "on-device first, Simplismart when the device can't". Micromax investing in Simplismart's Series B suggests Simplismart may want a device story; that is both a validation and a risk (see risks).

What we cannot claim: we will never beat them on tokens/sec/GPU, we have no custom kernels, and if their customers' workloads are 70B-class we are not an alternative.

### Moat

Honest version: at month 8 the moat is zero. Everything in the build pipeline is wrappers over llama.cpp, ExecuTorch, MLX, torchao and lm-eval. What compounds after that, in order of credibility:

1. **The device x model x quant benchmark corpus.** Nobody publishes "Gemma-4-E4B Q4_K_M on a Dimensity 7050 with 6 GB: 7.1 tok/s sustained, 3.9 GB RSS, 99.2% IFEval recovery, -1.8 pts on Hindi". After 12 months of certifying customer builds across 50+ SoCs and every notable small model, that table is a proprietary dataset that drives the manifest resolver, the "Can I run it?" hub, and sales. Platform vendors benchmark their own silicon only.
2. **Switching cost in the release loop.** Once a customer's fine-tune -> QAD -> certify -> OTA -> telemetry pipeline is in Fewbit, with per-SoC rollouts and adapter OTA wired into their app release train, ripping it out is a quarter of mobile-engineering work. Firebase's moat was never technical either.
3. **Fleet telemetry network effects.** Every device reporting perf/thermal/crash data improves resolver rules for every other customer on the same SoC class. This is the one asset Ollama, Cactus and NimbleEdge do not accumulate at the per-SoC accuracy level.
4. **Indic calibration and evaluation sets.** Thin today, unstudied in the literature ("multilingual quantization tax"), and nobody (Sarvam included) ships Indic-calibrated quant recipes with eval deltas. Cheap for us to build, annoying for a US company to replicate.
5. **Distribution deals** with OEMs/ISVs (Micromax/Lava/Jio-class, kiosk makers, Jetson integrators) that pre-install the SDK or ship certified builds. Hard to get, sticky if won.

What is not a moat: quantization algorithms (Red Hat, NVIDIA, Intel, Google own them), kernels (Arm, Qualcomm, Apple, ggml), and the hub itself (Unsloth gives quants away). The likely terminal outcome is acquisition by a chip or platform vendor (Qualcomm bought Edge Impulse and Modular; Rebellions bought SqueezeBits; NVIDIA bought Deci/OctoAI; Apple talked to PrismML) at $5-50M, or a durable $3-10M ARR niche business. Plan the company for that, not for a $1B outcome.

### 8-week MVP

Assumes 2 people (founder: ML/systems/Python; mobile engineer: Kotlin/Swift/C++) and the device rack bought in week 1. A third person (backend/devrel) accelerates weeks 6-8 but is not required.

**Week 1 - Pipeline skeleton + rack.**
- Buy devices (list in architecture). Set up adb/idevice automation and a Mac mini CI runner.
- Pin versions: llama.cpp (commit with KleidiAI SME2 + Q4_0 repack), ExecuTorch 1.5.1, mlx-lm, lm-eval 0.4.13, torchao 0.18.
- `fewbit build` v0 for GGUF only: HF -> BF16 GGUF -> imatrix on a 1M-token generic+Indic corpus -> Q4_0/Q4_K_M/IQ4_XS/Q5_K_M/Q6_K/Q8_0.
- Models: Gemma 4 E2B/E4B (QAT and non-QAT), Qwen3.5-1.7B/4B, Llama-3.2-3B, Sarvam-1 2B.
- Deliverable: 36 GGUF variants built reproducibly from a YAML.

**Week 2 - Accuracy + perf gate v0, first published numbers.**
- KLD runner (`llama-perplexity --kl-divergence-base` vs BF16 logits). lm-eval via llama-server OpenAI backend: IFEval, GSM8K-200, MMLU-Redux-500, HellaSwag-500; MILU-500 and IndicGenBench XL-Sum (hi, ta) subsets; BFCL-lite JSON validity.
- Device perf runner: llama-bench + 5-minute sustained decode + RSS + thermal via adb on 6 Androids, iPhone, Mac, Jetson, Pi 5.
- Eval-card JSON schema + Markdown renderer. Publish first 12 cards and GGUFs to the `fewbit` HF org.
- Deliverable: public "On-device LLMs on Indian phones, Oct 2026" table (tok/s and recovery for ~40 phone x model x quant cells). This is the launch asset.

**Week 3 - Automatic escalation + multi-target export.**
- Sensitivity scan (per-block KLD at 4-bit) -> per-tensor override map for llama-quantize.
- Escalation loop: build lowest precision, gate, escalate failing tensors then globally, stop at pass.
- ExecuTorch export (8da4w XNNPACK; attempt QNN 16a4w on the S25 and document the pain honestly), MLX export, Olive int4 ONNX export.
- `fewbit certify` runs the whole thing from one command; cards Ed25519-signed.

**Week 4 - Android SDK.**
- `fewbit-core`: thin C++ over llama.cpp's C API (load, chat-template, stream, LoRA adapter attach, KV Q8_0), prebuilt arm64-v8a with KleidiAI.
- Kotlin SDK: `Fewbit.init`, `models.resolve` (local stub), `load`, `stream`, tools; download manager with resume + chunk hashes + signature verify; sample app (chat + offline summariser).
- ExecuTorch runner behind the same interface for the QNN variant (flag-gated).

**Week 5 - iOS/macOS + Python SDKs.**
- Swift Package wrapping an xcframework of fewbit-core (Metal); same API; sample app.
- Python SDK: `fewbit.Fleet(...).resolve()` returns a local OpenAI-compatible server (llama-server subprocess) for Jetson/kiosk/Linux; verified on Orin Nano Super and Pi 5.
- Docs site v0 (mkdocs): quickstart per platform in <10 minutes.

**Week 6 - Control plane.**
- FastAPI + Postgres + R2: models/versions/variants/cards, device registration with capability fingerprint, `/resolve` manifest with deterministic rules (RAM floor = weights + KV at 4k + 1.2 GB headroom; NPU variant only if certified for exact SoC+driver), rollouts by % / app version / SoC, rollback, signed manifests. Helm chart for on-prem.
- CLI `publish`, `rollout`, `rollback` wired end-to-end.

**Week 7 - Telemetry, adapter OTA, dashboard, pricing.**
- SDK telemetry batcher (perf, errors, thermal, optional canary probes); ingest to Postgres; dashboard (fleet by variant/SoC, perf percentiles, rollout health).
- LoRA adapter OTA: publish a GGUF adapter as a version, resolver sends base+adapter, SDK attaches at load.
- Pricing page, Stripe/Razorpay, API keys, free tier limits.

**Week 8 - Two design-partner pilots + launch.**
- Pilot A (consumer Indic app or OEM): their fine-tune or Sarvam-1/Gemma-4 E4B -> certify in hi/ta -> OTA to 50-200 internal devices across 3 SoC classes -> telemetry review.
- Pilot B (Jetson robotics or kiosk): Qwen3-VL-4B or Gemma-4 E4B on Orin Nano Super, air-gapped registry via Helm.
- Launch: open-source repos (SDK, CLI, core), the benchmark report, HN/X/LinkedIn, Show HN, Indian dev communities; apply to Peak XV Surge / Antler / YC with pilot data.
- Deliverable: one paying pilot (even Rs 2-5 lakh) or two signed LOIs; 500+ GitHub stars is the vanity target, 20 inbound design-partner conversations is the real one.

Explicitly deferred past week 8: Windows NPU SDK polish, browser/WebGPU, ternary QAT service, LLM-judge evals beyond exact-match, SOC2.

### GTM

**Motion: open-core developer pull + founder-led enterprise sales in India, global via GitHub.**

Free (Apache-2.0 + hosted free tier): SDKs, CLI, hub of certified public models, fleet up to 2,000 monthly active devices (MAD), public models only, 7-day telemetry. Purpose: become the default way to put llama.cpp/ExecuTorch in an app without thinking.

Paid:
- **Team**: $199/month, up to 25k MAD, private models, OTA, 90-day telemetry.
- **Scale**: $5 per 1,000 MAD per month ($0.005/MAD), volume-discounted to ~$2 per 1,000 above 1M MAD. Sanity check vs cloud: a user generating 100k tokens/month on Simplismart's Gemma-3-1B costs $0.006, so per-device pricing is at or below the cloud bill for average users and far below for heavy voice/assistant use (1M tokens/user/month = $0.06-0.13 on cloud vs $0.005 here). The pitch to CFOs is cost at scale; the pitch to engineers is offline/privacy/latency.
- **Certification service**: Rs 3-8 lakh ($4-10k) per model per target set (PTQ + gate + cards) and Rs 8-20 lakh ($10-25k) with QAD. Cash-flow positive from month 3 if 2-3 of these close; this funds the company before Fleet revenue matters.
- **Enterprise**: $40-150k/year: on-prem control plane (Helm), custom QAD, SLA on certification turnaround, DPDP/HIPAA documentation, named SoC coverage.
- Realistic 18-month target: $300-600k ARR from 6-10 enterprise/certification customers plus long-tail Team/Scale. Nota AI's ~$5.9M revenue as a public company is the warning that tooling revenue is small; Fleet (per-device recurring) is what makes this bigger than a services shop.

**First 10 calls (hypotheses about fit; ordered by reachability from Bengaluru):**
1. **Sarvam AI** - partner, not customer: certify Indic quant builds of Sarvam-1 2B and their 30B at INT4 for CPU; co-publish Indic eval deltas. Gives credibility and a distribution channel.
2. **Micromax** (just invested in Simplismart) and **Lava** - budget-Android OEMs wanting an "AI assistant" that runs on 6 GB phones; OEM pre-install is the dream deal.
3. **Jio Platforms** (JioBharat/JioPC/JioBrain teams) - lowest-end devices, massive fleet, offline-first.
4. **Khushi Baby** (Rajasthan CHW app, offline-first) and **eGov Foundation/DIGIT** implementers - field-health and governance apps where on-device summarisation/form assistance under DPDP is a real need; grant-funded, patient buyers.
5. **Slang Labs / Gnani.ai** - in-app vernacular voice; on-device NLU and small-LLM intent routing cut their per-call cloud cost to zero.
6. **Pine Labs / Paytm devices team** - POS and soundbox-adjacent hardware; a certified 1B on a fixed SoC is a product, not a model.
7. **ideaForge / Garuda Aerospace / Addverb** - drones and warehouse robots on Jetson needing air-gapped VLMs.
8. **Tata Motors / Mahindra Electric / Ather** infotainment teams - offline in-car assistant on fixed SoCs with multi-year OTA obligations (long cycles; start now).
9. **Brave (Leo BYOM), Proton, Obsidian/Logseq plugin ecosystems** - global privacy-first software with existing local-model users; SDK adoption and hub traffic.
10. **HCLTech / Infosys internal AI platform teams** - Copilot+/Snapdragon X laptops for regulated clients; CPU-only on-prem assistants; also a channel to banks.

**Channels**: the benchmark report (refreshed quarterly) as the SEO/HN asset; llama.cpp/ExecuTorch/MLX community presence (PRs for KleidiAI/QNN fixes buy goodwill); Qualcomm AI Hub and Arm developer program listings; IndiaAI Mission and NASSCOM DeepTech for enterprise intros; a monthly "state of on-device LLMs on Indian phones" post.

### Team and cost

**Team (1-3 people, Bengaluru hypothesis)**
- Founder/CEO-CTO: ML systems + Python; owns build/certify pipeline, control plane, sales.
- Mobile/systems engineer (hire 1): Kotlin + Swift + C++/JNI, has shipped an app with native libs; owns fewbit-core and SDKs. This is the critical hire; without it the product is a CLI.
- Optional third (month 4+): backend/devrel; owns dashboard, docs, community, device-farm automation.
- Advisors to recruit (equity only): one llama.cpp/ggml or ExecuTorch contributor; one Qualcomm/MediaTek/Arm ecosystem person; one Indian mobile-app CTO.

**One-off**: device rack Rs 6-7 lakh (~$7-8k); company setup, trademarks, Apple/Play developer accounts ~Rs 1 lakh.

**Monthly burn (3 people)**: salaries Rs 5-7 lakh ($6-8.5k) for senior Bengaluru engineers at below-market cash + meaningful equity; cloud Rs 40-70k ($500-850): E2E L4 at Rs 49/hr for ~60 build hours, H100 at Rs 379/hr for ~20 QAT hours, Hetzner/E2E control plane $60, Cloudflare R2 1-3 TB at $0.015/GB (egress free, which matters for 2 GB model downloads), Firebase Test Lab/AWS Device Farm ~$150, GitHub Actions; SaaS/tools Rs 20k. Total ~Rs 6.5-8.5 lakh/month ($8-10k).

**12-month need**: ~Rs 1-1.2 Cr ($120-150k) including rack and buffer. Sources: certification services from month 3 (2-3 projects at Rs 3-8 lakh each cover a quarter of burn), angels/Antler/Peak XV Surge-style pre-seed ($250-500k) after the week-8 launch with pilot data. Do not raise a Simplismart-size round for this; the business does not need GPUs and the exit math does not support it.

**Not needed**: GPU fleet, kernel engineers, a sales team before $300k ARR.

### Why now

1. **Small models crossed the usefulness line and ship pre-quantized.** Gemma 4 QAT (Jun 2026) for E2B-31B with Q4_0/w4a16 and drafters, Qwen3.5 0.8B-4B, Llama 3.2 1B/3B with SpinQuant/QLoRA builds, BitNet b1.58-2B-4T, Falcon-E: a 2-4B model now does summarisation, extraction, tool calls and Indic chat well enough for product features, and the labs did the QAT.
2. **Runtimes matured in the last 12 months.** ExecuTorch 1.5 (Sep 2026) is in Instagram/WhatsApp/Quest with QNN QAD and Arm int8 KV; llama.cpp has KleidiAI SME2 and Q4_0 repack paths; MLX on M5; ORT GenAI covers Windows NPUs; bitnet.cpp got its 2026 CPU optimizations. The kernels are free; what is missing is the workflow.
3. **Silicon caught up.** Snapdragon 8 Elite Gen 5 does ~32 tok/s on a 3B w4a16; 2025-26 Arm cores ship SME2; Copilot+ PCs and Apple M4/M5 are everywhere in enterprise; Jetson Orin Nano Super is $249; India's mid-range moved to 8 GB RAM.
4. **Regulation and sovereignty pull.** India's DPDP Act rules were notified in late 2025 with phased compliance through 2026-27 (verify exact dates), IndiaAI Mission is funding sovereign stacks, and on-device is the simplest DPDP story there is: the data never leaves.
5. **The market just validated both ends.** Simplismart ($14M, NVIDIA) proves Indian inference infra can be built and funded from Bengaluru; Ollama ($65M), PrismML (Khosla, Apple talks), Multiverse ($570M), Qualcomm buying Edge Impulse and Modular, Rebellions buying SqueezeBits prove acquirers want edge/compression tooling. Micromax, a phone OEM, is now on Simplismart's cap table: the OEM appetite for an AI feature on budget devices is visible.
6. **Quantization research has a clear edge-shaped frontier.** QAT/QAD recipes (Gemma 3/4, ParetoQ), ternary kernels, and the documented failure modes for small/multilingual/reasoning models mean there is now a defined problem ('is my 4-bit build still correct on my phone in my language') with enough tooling to answer it automatically, and nobody packaging the answer.
7. **Cloud tokens got too cheap to compete with, which is exactly why not to.** At $0.05-0.14/M for 8B models, token resale is dead for a small entrant; the only places a two-person team can own are offline, private, zero-marginal-cost and under-served hardware, which is this.

### Risks

- Platform vendors commoditize the generic path: Apple Foundation Models (~3B, free, adapter-trainable), Google Gemini Nano via ML Kit/AICore and Gemma 4 QAT, Microsoft Phi Silica/Foundry Local, Qualcomm AI Hub (now with Edge Impulse and Modular) could make 'good enough on-device' a free OS feature; Fewbit survives only where customers need custom models across mixed fleets.
- Direct competitors already exist and some are funded: Ollama ($65M, 8.9M monthly devs, moving to hybrid local+cloud), NimbleEdge (Bengaluru, DeliteAI on-device platform), Cactus (YC on-device framework), Picovoice picoLLM, Nexa AI (NexaSDK on Hexagon), MLC-LLM/WebLLM; none does certification+fleet, but any could add it in a quarter.
- Accuracy at 4-bit is worst exactly where edge customers need it (<=4B models, Indic languages, reasoning): INT4 ~94% recovery on a 1.5B reasoning model, 2-bit collapses 1B models, low-resource languages lose more; the 'certified' promise may frequently resolve to 'use Q8 and a 1B model', which is a weak story.
- Mass-market Indian hardware may be too slow for the UX bar: 6 GB Dimensity/Snapdragon 6-series phones sustaining 3-8 tok/s with thermal throttling; the product could end up flagship-only, which shrinks the India thesis to the same premium users cloud already serves well.
- NPU toolchain churn and lock-in: Qualcomm GenieX still 'developer preview' with accuracy issues, hour-long conversions, per-SoC/driver certification that OS updates can invalidate, MediaTek NeuroPilot and Intel/AMD NPU paths each different; NPU support may cost more engineering than it returns for a 2-person team.
- Tooling churn in dependencies: AutoAWQ/AutoGPTQ/optimum-quanto died within 18 months, torchao is minimizing new features, TensorRT-LLM dropped its engine backend; Fewbit's value includes absorbing this churn, but it is also a permanent maintenance tax on a tiny team.
- Distribution of GB-scale models is a product problem we do not fully control: 1.5-2.5 GB downloads over Indian mobile data, app-store asset-delivery limits, storage-constrained phones, and user abandonment could cap adoption regardless of model quality.
- Weight-license and redistribution constraints (Gemma, Llama, Qwen variants, Sarvam) complicate a public hub of certified builds and enterprise redistribution; a license misstep with Google or Meta is existential for a small company.
- Revenue ceiling: compression/edge tooling companies are small even when public (Nota AI ~$5.9M revenue at a ~$462M IPO; Pruna ~$2.8M); per-device pricing must compete with sub-cent cloud tokens, so the realistic outcome is a $3-10M ARR business or a $5-50M acquisition, not a venture-scale company; raise and staff accordingly.
- Simplismart itself: Micromax joining its Series B hints at a device/edge extension; a funded incumbent with NVIDIA ties adding an 'edge' SKU would compete for the same Indian OEM and kiosk accounts.
- Founder bandwidth: the plan needs a strong native mobile engineer; if the first hire fails, the product is a CLI and a hub, which has no revenue model beyond services.


---

## Design [serving]: Nibble (working title; a nibble is 4 bits). Alternative: "Lowbit Serve".

**One-liner:** Dedicated, BYOC and air-gapped endpoints that serve 1B-72B open LLMs (and Whisper) on L4 / L40S / A10G / A100-class GPUs in India at FP8, INT8 W8A8 or W4A16 with FP8 KV cache and speculative decoding, where every endpoint ships a signed accuracy card against BF16 and a precision-pinned SLA, at 40-70% lower monthly cost than H100-based serving for the same workload.

**Target customer:** Primary: India- and SE-Asia-based B2B teams that already run (or want to run) open models in production and pay $2k-$60k/month for GPUs: voice bots and contact-centre automation (Gnani.ai, Skit.ai, Yellow.ai-class, and the dozens of smaller Indic voice-bot shops), document-AI in BFSI and legal (Perfios, SpotDraft-class), edtech doubt-solving at high volume/low ARPU (Physics Wallah-class), health-records apps under DPDP (Eka Care-class), and Indic-language app builders on Sarvam 30B / Gemma 4 / Qwen3.x. They serve 1B-32B models (occasionally 70B), run 10M-5B tokens/day, are latency-bound rather than throughput-bound (their dedicated GPUs sit at 10-30% utilisation), and need ap-south data residency. Secondary: regulated buyers (NBFCs, banks under RBI outsourcing rules, hospitals, PSUs, state governments using IndiaAI Mission GPU allotments) who need on-prem or air-gapped serving of small models and will pay an annual licence. Tertiary (inbound only): indie/YC-stage teams anywhere spending $5-20k/month on Fireworks/Baseten dedicated H100s for an 8B-14B model, reached through OpenRouter listings with disclosed precision. Explicitly NOT the customer: anyone whose bill is dominated by serverless tokens on popular models (DeepInfra/Groq at $0.02-0.08/M wins), diffusion/video generation (fal, Simplismart's InVideo/HeyGen/Higgsfield base), and frontier-scale MoE (DeepSeek-V4-Pro, Kimi K3) which needs multi-H100/B200 nodes we will not own.

**Problem:** 1) The mid-market overpays by 2-3x because serving defaults are H100 + BF16/FP16: Simplismart's default config is float16, its docs say FP8 is unavailable on A100/A10G, and its cheapest INT4 win (Sanas, H100 -> A10G, -53%) was a bespoke engagement, not a product. Baseten bills H100 at ~$6.50/hr, Fireworks ~$7/hr, Simplismart $4/hr; a 15-concurrent-user support bot on Qwen3-8B needs maybe 300-700 tok/s aggregate, which an L40S (E2E Networks $1.20/hr raw) delivers at FP8 (Red Hat measured 830 out tok/s on Llama-3.1-8B INT8 W8A8 on one L40S at max load). 2) Precision is undisclosed: a 2026 audit found only DeepInfra and Baseten label precision on OpenRouter; "silent quantization" is now a named governance complaint; no vendor contract covers FP16-vs-FP8, let alone accuracy. Simplismart does not say what its $0.13/M Llama-8B serverless endpoint actually runs. 3) Nobody sells an accuracy-guaranteed quantized endpoint: the tooling exists (llm-compressor, ModelOpt AutoQuantize, Intel INC autotune, lm-eval) but customers stitch it by hand and still get surprised (AWQ on Qwen2-VL-2B collapsed 67.2 -> 7.9; 3-bit KV loses ~20 pts on reasoning; FP8 KV needs sliding-window layers skipped on Gemma/gpt-oss). 4) India-specific: DPDP and RBI rules push BFSI/health to ap-south or on-prem; Indian GPU clouds (E2E, Neysa, Yotta, Jarvislabs) sell raw GPU-hours with no quantization-aware serving layer; Simplismart now books >50% revenue in the US and prices BYOC/on-prem by quote; Indic-language quantization degradation (AWQ-int4 -4.7%, GPTQ-int4 -3.8% on low-resource languages in an EMNLP 2025 benchmark) is unmeasured by every host. 5) Toolkit churn is itself the pain: AutoAWQ and AutoGPTQ died in 2025, optimum-quanto and TorchAO are in maintenance mode, llm-compressor ships breaking changes monthly, ModelOpt changed MoE checkpoint formats in 0.47. A customer wants a pinned, tested artifact plus launch flags, not a library.

### Product

## What it is
A serving platform where the unit of sale is a **dedicated endpoint on right-sized, cheap GPUs**, and the unit of trust is a **signed accuracy card**. Three deployment modes, one artifact format, one control plane.

### Deployment modes
1. **Managed dedicated (India region)**: we rent GPUs at E2E Networks / Neysa / Jarvislabs (ap-south), run vLLM per tenant in an isolated namespace, bill per replica-minute. No shared tenancy on a GPU.
2. **BYOC**: Helm chart + a small agent into the customer's EKS (ap-south-1), GKE (asia-south1), AKS (Central India) or on-prem k8s. Prompts never leave their VPC; we see metrics and the artifact manifest only.
3. **Air-gapped**: a single OCI/k3s bundle (vLLM image, artifacts, gateway, Grafana) with an offline Ed25519-signed licence, zero callbacks, quarterly refresh media. Same dashboard, same cards.

### UX (CLI first, dashboard second)
```
nibble plan  --model Qwen/Qwen3-8B --slo "p95_ttft<500ms,p95_itl<35ms,concurrency=16" \
             --context 8k --budget "max_usd_per_hour=2.0" --eval ./my_eval.jsonl
# -> prints 3 candidate recipes with predicted cost, perf and recovery:
#    [A] L40S  FP8_DYNAMIC + KV-FP8 + EAGLE3   $1.95/hr  est 820 tok/s  card: pending
#    [B] A10G  W4A16-GPTQ  + KV-FP8 + EAGLE3   $1.60/hr  est 380 tok/s  card: GOLD (99.3%)
#    [C] A100  INT8 W8A8   + KV-FP8            $3.10/hr  est 1,400 tok/s card: GOLD (99.6%)
nibble deploy --recipe A --region in-blr --replicas 1          # runs quantize -> eval gate -> card -> deploy
nibble card   dep_01HX...                                      # prints/opens the signed accuracy card
```
If a (model, recipe, hardware) card already exists in our public ledger, deploy is minutes; otherwise the Recipe Factory quantizes and evaluates first (2-8 GPU-hours for an 8B).

### API surface
- **Inference (OpenAI-compatible)**: `POST /v1/chat/completions`, `/v1/completions`, `/v1/embeddings`, `/v1/audio/transcriptions` (Whisper v3 Turbo via vLLM), streaming, tool calling, JSON schema (xgrammar), multi-LoRA (`model: "base:adapter-name"`). Every response carries `x-nibble-precision: w8a8-fp8;kv-fp8;spec-eagle3`, `x-nibble-recipe: sha256:...`, `x-nibble-card: https://.../cards/<id>`.
- **Control plane**: `POST /v1/plans` (recipe search), `POST /v1/deployments`, `GET /v1/deployments/{id}` (status, replicas, precision pin), `GET /v1/deployments/{id}/card`, `GET /v1/deployments/{id}/metrics` (TTFT/ITL/tok/s/$ per 1M tokens), `POST /v1/evals` (upload customer JSONL, exact-match / LLM-judge / regex graders), `POST /v1/artifacts/{id}/promote` (customer approves a precision change), `GET /v1/ledger` (public cards).
- **Accuracy card (JSON + HTML, cosign-signed)**: model + revision hash; recipe (scheme, group size, calibration set hash and size, ignore list, KV scheme); engine + kernel versions and exact vLLM launch flags; hardware; per-task scores vs BF16 reference with recovery %, stderr and seed; mean/99th-pct KL divergence vs BF16 on 2,000 held-out prompts; long-context (NIAH 32k, MRCR at max served context); reasoning extras (AIME24/GPQA-Diamond, CoT-length ratio) when applicable; Indic block (MILU, IndicGenBench Flores-In chrF) when applicable; customer eval score if supplied; GuideLLM perf table at 3 request rates; grade GOLD (mean recovery >= 99.0%, min task >= 97.0%, KL <= 0.02) or SILVER (>= 98% / >= 95%, opt-in only).

### SLA terms (the actual differentiator)
- **Precision pin**: the served precision/recipe hash cannot change without a new card and explicit customer promotion. Breach = 25% monthly credit.
- **Accuracy floor**: endpoint keeps its card grade; weekly drift check (500 sampled prod prompts, KL vs BF16 shadow run). If it falls below grade or below the customer's own eval threshold, we roll back to the next-higher precision at no extra charge for 30 days.
- **Latency SLO** per endpoint (p95 TTFT / ITL at the declared concurrency), measured by our gateway, credits at 10%/25%.
- **Uptime**: 99.5% at launch (honest for a 1-2 person team), 99.9% once there is a second on-call engineer.
- **Residency**: in-blr / ap-south only unless the customer opts into another region.

### Pricing (per replica-minute, GPU included, no minimum, managed India region)
| SKU | VRAM | Raw India rate (E2E/AWS ap-south, Oct 2026) | Nibble managed | Typical fit |
|---|---|---|---|---|
| L4 | 24 GB | ~$0.58/hr (Rs 49) | **$0.95/hr** | 1-4B FP8 (voice bots), Whisper |
| A10G | 24 GB | ~$1.21/hr (g5 on-demand) | **$1.60/hr** | 4-8B W4A16 / INT8 |
| L40S | 48 GB | $1.20/hr | **$1.95/hr** | 8-32B FP8, 70B W4A16 low-concurrency |
| A100-80 | 80 GB | $2.10/hr | **$3.10/hr** | 30-70B INT8 W8A8 |
| H100 | 80 GB | $3.99/hr | **$4.90/hr** | 70B+ FP8 only; planner will tell you if a cheaper tier passes the gate |

- **BYOC**: $0.25 per GPU-hour software fee (~$180/GPU-month) + $1,500/month platform minimum; includes cards, recipe refreshes, dashboard, drift monitoring. (Red Hat AI Inference Server lists ~$2,500/yr per accelerator but ships no cards, planner or SLA.)
- **Air-gapped / on-prem licence**: $48k/yr per site up to 8 GPUs, +$6k/GPU/yr beyond; includes quarterly refresh and two custom eval suites.
- **Card-only SKU** (top of funnel): $299 per model x recipe x hardware on standard suites; $999 including the customer's own eval set. Deliverable is the signed card plus launch flags; they can run it anywhere.
- **No serverless per-token tier at launch.** A free shared evaluation endpoint (1M tokens) exists for trials only; we do not fight DeepInfra/Groq on $/M.

### Worked unit economics (estimates to be validated in weeks 1-2; vendor-reported baselines)
- **Support bot, Qwen3-8B, 1.5k in / 250 out, peak 15 concurrent**: Simplismart dedicated H100 FP16 $4.00/hr = $2,920/mo (~15% utilised); Baseten H100 $6.50/hr = $4,745/mo. Nibble: 1x L40S FP8_DYNAMIC + KV-FP8 + EAGLE-3 at $1.95/hr = $1,424/mo, ~800 tok/s saturated capacity (Red Hat L40S INT8 datapoint: 830). Savings 51% / 70%.
- **Llama-3.3-70B assistant, <= 4 concurrent, 8k context**: 1x L40S W4A16-GPTQ (~37 GB weights, FP8 KV ~160 KB/token leaves ~50k tokens of cache) with EAGLE-3 at $1.95/hr vs 1x H100 FP8 at $4.00-6.50/hr. Savings 51-70%; decode ~20 tok/s raw, ~35-45 with spec decode (bandwidth-bound; acceptable for assistants, not for bulk generation).
- **Voice bot LLM pass, Gemma 4 E4B / Qwen3-4B FP8 on L4** ($0.95/hr = $694/mo) with official Gemma 4 drafter, p95 ITL < 20 ms at batch <= 8, plus Whisper v3 Turbo on the same card, vs A10G at Simplismart $2.00/hr ($1,460/mo). Savings 52%.
- Where H100 FP8 at full batch beats us per token (bulk/offline generation above ~2,000 tok/s per endpoint), the planner says so and offers the H100 SKU. We win on right-sizing, not on peak throughput.

### Explicitly out of scope (the "quantized" scope)
Text LLMs + Whisper only; 1B-72B dense and <=30B-active MoE; six GPU SKUs; India/ap-south regions; no diffusion/video, no training/fine-tuning (bring an Unsloth/Axolotl adapter, we serve multi-LoRA), no custom kernels, no edge/mobile.

### Technical architecture

## Components (all OSS unless noted; licences in brackets)
1. **nibble-cli / Recipe Planner** [Apache-2.0, open-sourced]: Python. Inputs: model id, hardware fleet, SLO, budget, optional eval set. Looks up the public ledger; if no card, proposes candidates from a rules table (see quantization strategy) and a cost model (per-SKU $/hr x predicted tok/s from GuideLLM history). Emits a recipe manifest (YAML) and vLLM launch flags.
2. **Recipe Factory** (quantize jobs): queue of GPU jobs on spot/on-demand E2E or AWS ap-south-1 g6e/p4d spot. Workers run **llm-compressor 0.14.x** (GPTQ W4A16, SmoothQuant+GPTQ INT8 W8A8, FP8_DYNAMIC / FP8_BLOCK, NVFP4, `kv_cache_scheme` FP8) emitting **compressed-tensors** safetensors; **Intel AutoRound** (AutoScheme mixed-bit) for quantization-sensitive small models and Indic models; **NVIDIA ModelOpt** only for Blackwell NVFP4 exports; **llama.cpp** `llama-imatrix` + `llama-quantize` for CPU/air-gapped GGUF. Calibration-set builder assembles 512 x 2048-token chat-templated samples: 50% customer prompts (opt-in, hashed), 25% domain corpus, 15% reasoning traces (model-generated), 10% Indic text when relevant; `add_special_tokens=False` at calibration, `add_bos_token=True` at eval.
3. **Eval Gate**: **lm-evaluation-harness 0.4.13** (vllm backend) for mmlu_pro (1k-item stratified subset), gsm8k 5-shot strict, ifeval, arc_challenge, hellaswag, truthfulqa_mc2, gpqa_diamond (reasoning models); **evalplus** for HumanEval+; **lighteval** for Indic tasks (MILU, IndicGenBench Flores-In); custom scripts for KL-divergence vs cached BF16 logits on 2,000 held-out prompts, NIAH 32k/128k and MRCR, CoT-length ratio; **GuideLLM** for constant / poisson / sweep load with TTFT, ITL, E2E distributions. BF16 reference scores are computed once per model revision on a rented H100 and cached. Output: accuracy card JSON + HTML, signed with **cosign** (Sigstore) keyless or an org key.
4. **Artifact Registry**: OCI artifacts via **ORAS** on **Harbor** (self-hosted) with a manifest per artifact: model hash, recipe, calibration hash, engine/kernel versions (vLLM, flash-attn, compressed-tensors, CUDA), hardware compat matrix (SM 8.0/8.6/8.9/9.0/10.0), launch flags, card id. Mirrored to a private Hugging Face org for BYOC pulls.
5. **Control Plane**: **FastAPI** + SQLModel/**Postgres** + **Redis** (arq job queue); tenants, deployments, artifacts, cards, metering, invoices (**Razorpay** for INR, **Stripe** for USD). Dashboard: HTMX + Tailwind (one person can maintain it); Grafana embedded for metrics.
6. **Data Plane (per tenant namespace on k8s)**: **vLLM 0.20+** pods via **Helm** (one chart, values per SKU), `--kv-cache-dtype fp8` with calibrated scales, `--kv-cache-dtype-skip-layers sliding_window` for Gemma/gpt-oss, `--speculative-config` (EAGLE-3 / official drafters / ngram), `--max-num-seqs` and `--max-model-len` from the plan; **SGLang** as the secondary engine for models where its kernels win (tested, not default). **Gateway**: FastAPI/uvicorn at launch (API keys, per-tenant rate limits, token metering, precision headers, request sampling for drift), migrate to **Envoy AI Gateway** above ~2k RPS. **Prometheus + Grafana + Loki + OpenTelemetry**; **KEDA** for replica scaling on queue depth with min replicas 1 (dedicated means no scale-to-zero by default; opt-in for dev endpoints). Clusters: **k3s** on E2E bare-metal/VM GPUs for managed; EKS/GKE/AKS for BYOC.
7. **BYOC Agent**: small Go binary deployed by the same Helm chart; pulls signed artifacts, verifies cosign signatures, applies vLLM manifests, pushes metrics (no prompt content) to our control plane over an outbound-only channel. Air-gapped: same chart packaged by `k3s` airgap + `docker save`, licence file checked locally.
8. **Drift Monitor**: weekly job samples 500 production prompts per endpoint (customer opt-in, PII-scrubbed with Presidio), replays on a 1-hour spot H100 BF16 shadow (~$4/week/model), computes KL and task-proxy deltas, updates the card's "last verified" block, pages if the grade drops.
9. **Public Precision Ledger**: static site + JSON API of every card we have produced; new open-model releases get FP8 / INT8 / W4A16 cards within 48 hours (this is the content engine).

## Data flow
`nibble deploy` -> control plane validates tenant + budget -> ledger lookup -> (miss) Recipe Factory job on spot GPU -> Eval Gate on target SKU + cached BF16 reference -> card signed and stored -> artifact pushed to Harbor/HF -> Helm release in tenant namespace (managed) or agent reconciles (BYOC) -> gateway registers route and precision headers -> GuideLLM smoke test against the live endpoint must meet SLO -> endpoint marked READY -> metering -> monthly invoice -> weekly drift job.

## Hardware tiers (what we actually rent, Oct 2026 list rates)
| Tier | SKU | Arch | Where | Precision used | Why |
|---|---|---|---|---|---|
| Cheap | L4 24 GB | Ada (SM 8.9) | E2E Rs 49/hr; GCP asia-south1 | FP8 W8A8, FP8 KV | Ada has FP8; ideal for 1-4B voice/Whisper |
| Cheap | A10G 24 GB | Ampere (SM 8.6) | AWS ap-south-1 g5 on-demand ~$1.21, spot ~$0.40 | INT8 W8A8, W4A16 (Marlin) | No FP8; INT8 keeps deltas < stderr |
| Core | L40S 48 GB | Ada | E2E $1.20/hr | FP8 W8A8, FP8 KV, W4A16 for 70B | QServe/Red Hat show L40S matching A100-class at low precision |
| Core | A100-80 | Ampere (SM 8.0) | E2E $2.10/hr | INT8 W8A8, W4A16 | Cheapest 80 GB in India; Simplismart cannot FP8 here |
| Peak | H100 | Hopper | E2E $3.99/hr | FP8, FP8 KV, NVFP4 weight-only (Marlin) for memory | 70B+ at throughput |
| Later | B200 / RTX PRO 6000 | Blackwell | E2E B200 $7.99/hr; SM120 immature | NVFP4 + FP8 KV for >=30B | Only when NVFP4 kernels on vLLM are stable for the model |
| Phase 2 | MI300X / MI355X | AMD CDNA3/4 | TensorWave/Vultr (not in India) | FP8 (vLLM ROCm), MXFP4 via Quark | 192 GB lets 70B FP8 fit on one GPU; US-region customers only |

Spot is used for quantize/eval jobs and shadow BF16 runs from day one, and for burst replicas (2-minute drain, min 1 on-demand replica) from month 4. CPU-only (llama.cpp Q4_0 QAT GGUF, bitnet.cpp) is offered only inside the air-gapped bundle for <=4B models.

## Stack summary
Python 3.12, FastAPI, SQLModel, Postgres 16, Redis/arq, vLLM, SGLang, llm-compressor, compressed-tensors, AutoRound, ModelOpt, llama.cpp, lm-evaluation-harness, lighteval, evalplus, GuideLLM, Presidio, Helm, k3s/EKS/GKE/AKS, KEDA, Harbor + ORAS, cosign, Prometheus/Grafana/Loki/OTel, HTMX dashboard, Razorpay/Stripe, Terraform for E2E/AWS provisioning. No custom CUDA. Everything proprietary is the planner rules, the ledger, the card format, the agent and the control plane.

### Quantization strategy

## Principle
Use only precisions with production kernels in vLLM on the GPU we are renting, and only where measured recovery clears the gate. Memory savings that do not translate into either a cheaper SKU or an SLO win are not used. Everything below is backed by numbers from the digest (ACL 2025 "Give Me BF16 or Give Me Death", Red Hat L40S INT8 study Sep 2026, vLLM FP8-KV study Apr 2026, vLLM TurboQuant study May 2026, COLM 2025 reasoning paper, Red Hat NVFP4 Feb 2026, SpecMQuant 2025).

## Decision table (weights x activations) by hardware
| Hardware | Default for <=14B | Default for 14-72B | Memory-fit fallback | Never |
|---|---|---|---|---|
| Ada / Hopper (L4, L40S, H100/H200) | **FP8_DYNAMIC** W8A8 (per-channel weight, per-token activation). ACL 2025: 8-bit ~99.75% recovery, FP8 effectively lossless | FP8_DYNAMIC; **FP8_BLOCK** (128x128) for MoE experts | **W4A16 GPTQ g128 -> Marlin** (99.36% mean recovery, worst task ~96.9%) when weights do not fit (70B on 1x L40S) | W4A4 (no production Hopper kernels); NVFP4 activations (Hopper has no FP4 cores; vLLM falls back to Marlin weight-only, so use it only for memory) |
| Ampere (A100, A10G, A30) | **INT8 W8A8** via SmoothQuant + GPTQ (Red Hat: Llama-3.1-8B deltas below benchmark stderr; 14.9 -> 8.0 GB) | INT8 W8A8 for 30B-class on A100-80; **W4A16** for 70B on A100-80 | W4A16 AWQ/GPTQ Marlin | FP8 (unsupported); 3-bit |
| Blackwell (B200, RTX PRO) | FP8 (NVFP4 recovery for 7-14B is only 95-98%, Llama-3.1-8B worst: below our GOLD gate) | **NVFP4** via llm-compressor (`QuantizationModifier(scheme="NVFP4")`, ~20 calibration samples, MSE/iMatrix scale observers) for >=30B: ~99% recovery at 70B-235B; ModelOpt export when TRT-LLM is required | - | SM120 consumer cards until TensorRT-LLM/llama.cpp correctness issues (#14154, #26704) are closed |
| Turing (T4) | W4A16 AWQ (no Marlin on Turing; slow) | not offered | - | Everything else; we do not list T4 |
| CPU (air-gapped only) | Vendor QAT Q4_0 GGUF (Gemma 4 QAT) via llama.cpp; BitNet b1.58 via bitnet.cpp for <=2B | not offered | - | PTQ'd GGUF below Q4_K_M |

## KV-cache policy
- **FP8 KV (e4m3) with calibrated per-head scales from llm-compressor** is the default when the served context >= 4k; the vLLM study shows per-token decode cost ~54% of BF16, +14.9% throughput at 20k-in on Llama-3.1-8B, break-even ~7k tokens, so endpoints capped at <= 4k context keep BF16 KV (no gain, small risk).
- Always pass `--kv-cache-dtype-skip-layers sliding_window` for Gemma 4 / gpt-oss-style models (128-token-window layers broke NIAH 91% -> 13% before the accumulation fix).
- head_dim-256 models (Gemma 4 E-series) get a TTFT check at 32k because FP8 KV raises the quadratic TTFT term ~1.6x; the gate may choose BF16 KV + smaller batch instead.
- MLA models (DeepSeek/Kimi-style) are calibrated, never uncalibrated FP8 KV (consistent drops observed with FlashMLA).
- **No sub-8-bit KV in production.** TurboQuant 4bit-nc (3.4x capacity, 1-4 pt loss, 66-80% of BF16 throughput) is offered only as an opt-in "long-context experimental" SILVER tier for >=128k RAG workloads; 3-bit variants are banned (~-20 pts on reasoning, ~-30% relative MRCR AUC).

## Speculative decoding policy
- Dedicated endpoints are mostly low-batch and latency-bound, which is exactly where spec decoding pays (EAGLE-3 + FP8 70B: 3.0-3.4x at batch 1 falling to ~1.16x at batch 32).
- Order of preference: official drafters (Gemma 4 ships them), published EAGLE-3 heads (yuhuili for Llama 3.x; community heads such as AngelSlim for Qwen3, verified by us), then `ngram` prompt-lookup for RAG/extraction workloads with high copy rates.
- On **W4A16 targets** we default to sequential (non-tree) drafting with 2-3 tokens, because tree verification erases the memory-bound gain (SpecMQuant: vanilla SD beat EAGLE-2 on W4A16 70B); EAGLE-3 trees stay on FP8/INT8 targets.
- Auto-disable: canary measures speedup per observed batch bucket; if < 1.15x at the endpoint's median batch, spec decoding is turned off and the card records it. Draft acceptance is logged in the card.

## Model-class rules
- **Reasoning / RL-trained models** (QwQ, R1-distills, Qwen3 thinking): never below 8-bit weights under 14B; W4A16 only >= 14B (COLM 2025: near-lossless only >= 14B; 3-bit AWQ -5.2 on QwQ-32B). Card must include AIME24 / GPQA-Diamond within 2 pts and **CoT-length ratio <= 1.10** vs BF16 (quantized reasoning models inflate chains). Calibration set gets 30% model-generated reasoning traces (ScaleQ-1.58 shows calibration-data reasoning content matters).
- **VLMs**: quantize language layers only; ViT and projector stay BF16 (AWQ collapsed Qwen2-VL-2B to 7.9 avg; Qwen3-VL official FP8 leaves ViT untouched).
- **MoE**: experts FP8_BLOCK; shared experts and routers stay BF16/FP8 never INT4 (shared experts reported disproportionately sensitive); per-expert scales; W4A16 experts only on >= 100B-total models with GOLD cards.
- **Native low-precision checkpoints** (Gemma 4 QAT w4a16, gpt-oss MXFP4, Kimi K3 MXFP4): serve the vendor checkpoint as-is on hardware with kernels (MXFP4 experts route via DeepGEMM fp8_fp4 on Hopper; Marlin fallback on Ampere), and still produce a card. We do not re-quantize what the lab already QAT'd.
- **Indic models** (Sarvam 30B, Gemma 4 for Hindi): INT8/FP8 default; W4A16 only if the Indic block passes (MILU and Flores-In chrF within 1.5% relative); AutoRound AutoScheme mixed-bit used when plain W4A16 fails (INT4 hurts low-resource languages 3.8-4.7% in EMNLP 2025 data). We will publish the first per-language quantization cards for Sarvam 30B.
- **QAT/QAD**: not a service we sell in the first 6 months (llm-compressor's QADModifier is available; Gemma 3 needed ~5,000 steps). Offered later as a paid recipe for customers whose W4A16 fails the gate on their eval set.

## Promotion gate (hard, automated)
1. Standard suite mean recovery vs BF16 >= 99.0% and minimum task >= 97.0% (GOLD); 98.0% / 95.0% (SILVER, customer must opt in and the header says so).
2. Mean KL(BF16 || quant) on 2,000 held-out domain prompts <= 0.02; 99th percentile <= 0.6 (reference: Unsloth Q4_K_M Qwen3.5 mean 0.0192, 99.9th pct 0.548).
3. NIAH 32k >= 95% of BF16 score; MRCR at the endpoint's max context within 2 pts.
4. Reasoning models: AIME24 and GPQA-Diamond within 2 pts; CoT-length ratio <= 1.10.
5. Customer eval set (>= 200 items) within the customer's declared tolerance (default 1.5 pts absolute).
6. GuideLLM constant-rate run at the declared concurrency meets p95 TTFT/ITL; otherwise the planner moves to the next candidate (higher precision, bigger SKU, or a second replica).
Any failure falls back automatically: W4A16 -> INT8/FP8 -> BF16 on a bigger SKU; the customer sees the cost difference before approving.

## Reference-point costs of the gate
BF16 reference for an 8B: ~1.5 H100-hours (~$6); quant + gate on target SKU: 2-4 GPU-hours (~$3-8 on L40S). For a 70B: ~8 H100-hours reference (~$32, cached forever per revision) and ~10 L40S-hours per recipe. Cheap enough to publish cards for every notable open-model release within 48 hours.

## Weekly drift
500 sampled production prompts (opt-in, Presidio-scrubbed) replayed on a 1-hour spot H100 BF16 shadow; KL and a 100-item task proxy recomputed; card "last verified" updated; grade drop pages us and triggers the rollback SLA.

### Differentiation vs Simplismart

1) Thesis vs feature. Simplismart sells "fewer GPUs per workload" through a closed engine (28 custom kernels, 140+ config options) whose default is float16; quantization is one knob, FP8 is unavailable on Ampere, and its only INT4 win (Sanas) was bespoke. Nibble's product IS the precision decision plus its proof: every endpoint is planned to the cheapest SKU that passes an accuracy gate, and the served precision is pinned in the contract.

2) Hardware wedge they do not emphasise. They price T4/L4/A10G/A100 at 1.5-2.5x raw India rates and push H100 ($4/hr, roughly E2E's raw price, implying their margin is elsewhere). We make L4 (Ada, FP8-capable, Rs 49/hr raw) and L40S ($1.20 raw) the default for 1-32B models and A100-80 INT8 W8A8 the default for 30-70B, where Simplismart cannot run FP8 at all. We do not list T4.

3) Transparency as product. Simplismart's benchmarks are single-user peaks with no methodology (501 vs 350 vs 343 tok/s depending on outlet) and no neutral audit; precision on its serverless endpoints is undisclosed. We publish reproducible GuideLLM runs with exact flags, signed cards, and precision headers on every response, and we submit to Artificial Analysis for the two or three models we host.

4) Open core. Simplismart has no open-source component and therefore zero community pull against vLLM/SGLang/llm-compressor. Our planner, card format and ledger are Apache-2.0; the public ledger ("what does Qwen3.7-14B lose at FP8 on an L40S?") is the inbound engine. This is the Pruna/Neural Magic playbook, not Simplismart's.

5) Contractual accuracy and precision pin. No vendor found, Simplismart included, offers precision disclosure or accuracy floors in SLAs. We do, with automatic rollback and credits.

6) India mid-market and regulated focus while they go US. Simplismart books >50% revenue in the US, quotes BYOC/on-prem, and is tied to Yotta (whose Shakti Studio runs on it). We rent at E2E/Neysa/Jarvislabs, bill in INR via Razorpay, publish list prices for BYOC and air-gapped, target IndiaAI Mission GPU allotments (Rs 67-92/GPU-hr) as a deployment target, and publish Indic-language cards (nobody does).

7) Narrower by design. Text LLMs + Whisper, 1B-72B, six SKUs, no diffusion/video, no training suite, no orchestration DSL, no custom kernels. Simplismart's biggest named customers (InVideo, HeyGen, Higgsfield) are video; we concede that market entirely.

Where Simplismart is simply better: raw engine throughput on H100 (custom kernels, Eagle-3, torch.compile); modality breadth; a 58-person team with NVIDIA/Accel/DVC and an existing US customer base; AWS/Azure Marketplace listings; the ability to copy "accuracy card" in a sprint if it ever matters to them.

### Moat

Honest answer: thin at launch, and kernels will never be it (Red Hat, NVIDIA, Intel and PyTorch own the algorithms and ship them free). What compounds:

1) The precision ledger as the reference dataset. Hundreds then thousands of signed cards (model x recipe x hardware x eval suite, including Indic, long-context and reasoning blocks, plus GuideLLM perf) with reproducible flags. Artificial Analysis became a brand by measuring providers; nobody measures precision. Once developers cite "Nibble GOLD" the way they cite Unsloth Dynamic quants, the ledger is both distribution and a data asset the planner's cost/recovery predictor trains on.

2) Customer-specific assets with switching cost: their eval sets, calibration corpora (hashed prompt samples), drift history and promoted recipes live in our registry; every quarter the recipes are re-validated on new engine versions. Leaving means re-doing the gate on another platform that does not have one.

3) Contractual trust and compliance surface: precision pin + accuracy floor clauses, DPDP/RBI-friendly residency, air-gapped licences with offline verification, SOC 2 Type I by month 9. Regulated on-prem deals are 2-3 year contracts with annual refresh media; those customers do not churn to a serverless API.

4) Capacity economics in India: 12-36 month commits at E2E/Neysa (H100 Rs 219/hr on 36-month vs Rs 379 on-demand; similar discounts on L40S/A100) once we have 20+ endpoints of base load; a solo founder cannot commit early, but by month 9-12 committed cheap Ampere/Ada capacity plus right-sizing is a 30-40% structural cost edge that pure software vendors (Red Hat AI Inference Server, Dynamo users) do not have and US clouds will not bother with.

5) Toolkit-churn absorption: a pinned, tested matrix (vLLM x llm-compressor x compressed-tensors x CUDA x SKU) for every artifact, refreshed weekly, is boring and valuable; the deaths of AutoAWQ/AutoGPTQ/quanto show customers pay to not track this.

What is NOT a moat and we should not pretend: the planner rules (copyable in weeks), the CLI, the OpenAI-compatible gateway, the Helm chart. If Simplismart or Baseten add precision headers and a card, the remaining edge is the ledger, India price points, regulated installs and the customer eval assets.

### 8-week MVP

## Assumptions
1 founder-engineer full time, optionally 1 contractor from week 3 (SRE/backend), total compute budget for 8 weeks ~$2,500-4,000. Models in scope for MVP: Qwen3-8B (or current Qwen3.x 8B), Llama-3.1-8B-Instruct (for comparability with Simplismart/Red Hat numbers), Gemma 4 12B or 26B-A4B (vendor QAT + drafters), Sarvam 30B (Indic), Llama-3.3-70B (memory-fit story). Hardware: E2E L40S + A100-80 on-demand, 1 H100 for BF16 references, AWS ap-south-1 g5 spot for A10G.

## Week 1: reproduce the numbers, pick the matrix
- Accounts at E2E Networks, Jarvislabs, AWS ap-south-1; Terraform for one L40S, one A100-80, one spot A10G; H100 by the hour only.
- Stand up vLLM 0.20+, llm-compressor 0.14.x, lm-eval 0.4.13, GuideLLM, evalplus, lighteval on a base image; pin every version in a lockfile.
- Reproduce Red Hat's L40S INT8/FP8 Llama-3.1-8B results (target ~800 out tok/s at max load, TTFT -19-24%) and the FP8 KV +14.9% result at 20k-in; verify FP8 KV behaviour on A100 (storage-only path) and the sliding-window skip on Gemma 4.
- Deliverable: internal table of tok/s and TTFT/ITL for 5 models x 3 precisions x 3 SKUs; the cost model's first data.

## Week 2: Recipe Factory v0
- `nibble quantize` CLI wrapping llm-compressor recipes (FP8_DYNAMIC, FP8_BLOCK, INT8 W8A8 SmoothQuant+GPTQ, W4A16 GPTQ g128, FP8 KV scheme) and AutoRound AutoScheme; calibration-set builder (512 x 2048 chat-templated, domain mix, hashed manifest); artifact manifest YAML; push to a self-hosted Harbor via ORAS plus a private HF org mirror.
- Quantize the 5 models; store BF16 reference logits on 2,000 held-out prompts from a 2-hour H100 run.
- Deliverable: 12 artifacts with manifests.

## Week 3: Eval Gate v0 and the accuracy card
- Gate runner: lm-eval tasks (mmlu_pro subset, gsm8k, ifeval, arc_challenge, hellaswag, truthfulqa_mc2, gpqa_diamond where relevant), evalplus HumanEval+, KL script, NIAH 32k, GuideLLM 3-rate profile; GOLD/SILVER grading logic; HTML + JSON card; cosign signing; `nibble card`.
- Run the gate on all 12 artifacts; expect at least one W4A16 failure (Llama-3.1-8B TruthfulQA ~96.9% worst case) to prove the gate bites.
- Deliverable: first 10+ signed cards, including Sarvam 30B INT8 vs W4A16 with MILU/Flores-In blocks (a genuinely new public datapoint).

## Week 4: first live endpoint
- Helm chart for vLLM per SKU with spec decoding (EAGLE-3 head for Llama 3.1 8B, Gemma 4 drafter), FP8 KV flags, KEDA min-1; k3s on an E2E L40S.
- Gateway (FastAPI): API keys, rate limits, token metering to Postgres, `x-nibble-*` headers, request sampling hook; Prometheus/Grafana dashboards for TTFT/ITL/tok/s/$ per 1M.
- Smoke-test rule: GuideLLM must meet the plan's SLO before READY.
- Deliverable: `https://api.<domain>/v1/chat/completions` serving Qwen3-8B FP8 on one L40S with a public card link in headers; the founder dogfoods it for a week.

## Week 5: control plane, dashboard, public ledger
- Deployments/plans/evals API, tenant model, Razorpay + Stripe metered billing, HTMX dashboard (endpoints, cards, cost, metrics), status page.
- `nibble plan` v0: rules table + cost model from week 1 data; prints 3 candidates.
- Public ledger site with the 10-15 cards and reproducible GuideLLM configs; open-source the CLI + card schema (Apache-2.0).
- Deliverable: a stranger can sign up, pick a model/SKU, see the card, deploy, and get billed.

## Week 6: BYOC and design partners
- Helm chart + agent for EKS ap-south-1 and GKE asia-south1 (outbound-only metrics, cosign verification, artifact pull from HF/Harbor); docs with a 30-minute install path.
- Start 3 design-partner pilots (targets from GTM list): one voice bot on L4/A10G, one document-AI on L40S, one BYOC in the customer's AWS; each gets a custom eval set wired into the gate.
- Deliverable: BYOC install succeeds on a clean EKS cluster; 3 pilots live with SLO dashboards.

## Week 7: hardening and SLA plumbing
- Health checks, pod restart/failover, node-loss drill on E2E, backups for Postgres/Harbor; drift job (weekly 500-prompt KL on a spot H100) running for pilots; precision-pin enforcement (deploy refuses recipe changes without `promote`); credits computation; PII scrubbing (Presidio) on sampled prompts; basic security review (per-tenant namespaces, secrets, no shared GPUs, audit log).
- Write the SLA document (99.5% uptime, precision pin, accuracy floor, latency SLO) and the DPA/DPDP addendum with a lawyer (Rs 50-80k).
- Deliverable: a 24-hour soak test at pilot load with zero manual intervention; SLA and DPA ready to sign.

## Week 8: launch
- Publish list pricing; a reproducible benchmark post ("Qwen3-8B on one L40S at FP8: 800 tok/s, GOLD card, $1.95/hr, full flags") contrasting vendor-reported single-user peaks; submit two hosted models to Artificial Analysis; Show HN + r/LocalLLaMA with the ledger; list two models on OpenRouter with precision labels (even if unprofitable, for distribution).
- Convert at least 1 of 3 pilots to paid (target Rs 1-2 lakh/month combined); sign the first Card-only SKU ($299-999) sales to people who will not host with us.
- Deliverable: paying revenue, 20+ public cards, a backlog of inbound from the ledger, and a decision memo on whether to hire engineer #2 or raise.

## Not in the 8 weeks (deliberately)
Air-gapped bundle (month 3-4, needs a signed customer), Blackwell NVFP4 (month 4-6, when SM100 kernels on the models we host are stable), AMD (month 5+, US customers), Whisper endpoints (month 3), SOC 2 (month 6-9), serverless.

### GTM

Motion: open-core content engine for inbound + founder-led outbound to 10 named accounts + Indian GPU clouds as channel. No paid marketing.

1) The ledger as the growth loop. Every notable open-model release (Qwen, Gemma, Llama, Sarvam, Mistral, gpt-oss) gets FP8 / INT8 / W4A16 cards on L4 / L40S / A100 within 48 hours, posted to r/LocalLLaMA, HN, X and a weekly "precision report" email. The angle is always a measured, reproducible claim against vendor-reported peaks ("Simplismart says 501 tok/s single-user on an H100; here is 800 tok/s aggregate on a $1.20/hr L40S at FP8 with the GOLD card and the flags"). Card-only SKU ($299-999) converts readers who will never host with us and seeds the eval-set relationship.

2) First 10 customers to call (hypotheses, India-first, all have a reason to care about cost, latency or residency):
   1. Gnani.ai (Bengaluru voice AI, Indic voice bots; latency-bound small models on expensive GPUs) - L4/A10G FP8 + spec decode pitch.
   2. Skit.ai (voice bots for collections; strict ITL budgets) - same pitch plus Whisper on the same card.
   3. Yellow.ai (serves its own Orion LLMs; large GPU bill; enterprise residency needs) - BYOC on their AWS ap-south-1.
   4. Perfios (BFSI document AI; RBI/DPDP; on-prem appetite) - BYOC now, air-gapped licence later.
   5. SpotDraft (legal contract extraction; long-context) - L40S FP8 + FP8 KV for 32k docs, MRCR block in the card.
   6. Physics Wallah (edtech doubt-solving in Hindi, high volume / low ARPU) - A100 INT8 for a 30B-class or L40S FP8 14B, Indic block.
   7. Eka Care (health records under DPDP) - BYOC with precision pin as a compliance artefact.
   8. Sarvam ecosystem app builders and Karya (Indic data/apps) - first Sarvam 30B cards as the door-opener; ask Sarvam for a co-published card.
   9. Shiprocket or Apna (existing Simplismart customers) - low probability, but a 30-minute call teaches us their price, precision disclosure and pain; offer a free card on their eval set.
   10. Channel: E2E Networks and Jarvislabs (marketplace listing / referral), Neysa (already partnered with Pipeshift, so a secondary target), and IndiaAI Mission-eligible institutions (IITs, AIIMS, state governments) who get Rs 67-92/GPU-hr allotments and need a serving layer for them.
   Plus two international lanes once there is a US region on AWS/Lambda spot: OpenRouter users who pick labelled-precision providers, and YC-stage teams on $5-20k/month Fireworks/Baseten dedicated H100s for 8-14B models (reach via the benchmark posts and the Card-only SKU).

3) Sales mechanics. Pilot = free 2-week dedicated endpoint on our GPUs with a card on the customer's eval set, then month-to-month. Pricing anchors on their current monthly GPU bill ("we will cut this 40-70% or you pay nothing"), not on $/M tokens. For regulated accounts: card + DPA + residency + air-gapped roadmap in the first meeting; expect 6-12 month cycles, so start those conversations in month 2 but do not plan revenue from them before month 9. Partners: Unsloth/Axolotl users bring adapters (we serve multi-LoRA), Red Hat-shops are not a target (they will buy RHAIIS).

4) Targets. Month 3: 5 paying endpoints, Rs 5-8 lakh MRR. Month 6: 20 endpoints + 2 BYOC, Rs 20-30 lakh MRR (~$25-35k). Month 12: 60 endpoints, 6 BYOC, 2 air-gapped licences, ~$100-120k MRR; that is the level where committed GPU capacity (and a Series-A conversation) makes sense. Mid-market Indian ACVs are $1-5k/month, so the ledger must generate volume; the air-gapped licences ($48k+) are where ACV comes from.

### Team and cost

Team. Person 1 (founder): backend/infra + ML tooling (FastAPI, k8s, vLLM, llm-compressor, eval harnesses); owns planner, gate, control plane. Person 2 (contract from week 3, full time by month 3): SRE/backend who takes on-call, Helm/BYOC agent, observability; without this person a 99.5% SLA is not credible. Person 3 (month 4-6, optional): founding solutions/GTM engineer who runs pilots, writes cards and posts, and sells to regulated accounts. No kernel engineers; we do not write CUDA.

Salaries (India, 2026): senior infra/ML engineer Rs 30-50 lakh/yr; so two engineers ~Rs 7-8 lakh/month; founder at minimal draw.

Compute. 8-week MVP: L40S ~400 h ($480), A100-80 ~250 h ($525), spot A10G ~200 h ($80), H100 for BF16 references and shadows ~150 h ($600), eval/quantize spot jobs ~$400, control-plane VMs/Postgres/Harbor ~$150 => ~$2,300-3,000, plus pilot endpoints (passed through at cost, ~$1,500/month for three). Steady state months 3-12: COGS = GPU rental billed through at ~1.5x raw (gross margin ~35-45% on managed, ~90% on BYOC/licence), shadow/drift ~$4/week/model, dev/eval GPUs ~Rs 1-2 lakh/month.

Monthly burn (2 engineers + compute + tools + legal/accounting): Rs 10-14 lakh (~$12-17k). 8-week MVP all-in: ~Rs 6-10 lakh with a contractor, ~Rs 2 lakh solo.

Capital. Bootstrap-able to month 3-4 on founder savings plus pilot revenue; to reach month 12 targets and hire #2/#3, raise $400-600k pre-seed (Titan Capital, Antler, Blume, Peak XV Surge, Shastra-type funds already backed Simplismart and Inferless; also IndiaAI Mission grants and NVIDIA Inception credits). Committed GPU capacity (Rs 20-40 lakh prepay for 12-month L40S/A100 commits) becomes worthwhile around 20 endpoints of base load and should come from revenue or a Series A, not pre-seed. One-off: SOC 2 Type I (~$20-30k incl. tooling) in month 6-9 only if a BFSI/health deal requires it; legal for SLA/DPA/licence (~Rs 1.5-2 lakh).

### Why now

1) The accuracy evidence is finally settled enough to put in a contract: ACL 2025 (500k+ evals) shows FP8 W8A8 lossless and W4A16 at ~99.4% mean recovery; Red Hat's Sep 2026 L40S INT8 study shows deltas below benchmark stderr with +44% throughput; the vLLM FP8-KV (Apr 2026) and TurboQuant (May 2026) studies give exact break-even and failure numbers. Two years ago a precision SLA would have been guesswork; today it is a lookup table plus a gate.

2) The tooling consolidated in the last 18 months: AutoAWQ/AutoGPTQ died, llm-compressor became vLLM's native quantization path with compressed-tensors loading directly, AutoRound merged in (Dec 2025 / Jan 2026) with mixed-bit search, ModelOpt AutoQuantize and KV AutoQuantize shipped (Aug-Oct 2026), lm-eval 0.4.13 and GuideLLM are stable. A 1-3 person team can assemble a production gate from Apache-2.0 parts without writing a kernel.

3) Cheap Ada/Ampere capacity in India is abundant and mispriced relative to its FP8/INT8 capability: L4 at Rs 49/hr, L40S $1.20, A100-80 $2.10 at E2E versus H100 $3.99-7.00 elsewhere; India's GPU count is heading from ~34k to a 100k target by Dec 2026 and IndiaAI Mission subsidises Rs 67-92/GPU-hr for eligible users who have no serving layer.

4) Regulation and disclosure pressure arrived: DPDP rules and RBI outsourcing guidance push BFSI/health to residency and on-prem; "silent quantization" became a named governance complaint in 2026 and a 2026 audit found only two OpenRouter providers label precision. Buyers are starting to ask what precision they are paying for; nobody has an answer in writing.

5) The category was just validated and its leader is moving away from the segment: Simplismart's $14M Series B (27 Oct 2026, NVIDIA/DVC/Accel) proves Indian buyers pay for inference optimisation, while Simplismart books >50% revenue in the US, prices BYOC by quote, lacks FP8 on Ampere, and ignores precision disclosure. Together/Fireworks/Baseten are chasing B200/NVFP4 and $10B+ valuations; the sub-$5k/month Indian endpoint is nobody's priority.

6) Native low-precision releases (Gemma 4 QAT with drafters, gpt-oss MXFP4, Kimi K3) make low precision mainstream and respectable, but they run badly or not at all on the cheap GPUs customers can afford; the gap between formats and kernels on Ampere/Ada/SM120 is exactly the right-sizing and verification work this product sells.

### Risks

- Token-price floor: serverless 8B tokens sell for $0.02-0.14/M (DeepInfra, Groq, Together Lite, Simplismart) and L40S FP8 math lands at ~$0.40-1.00/M at realistic utilisation, so the business is dedicated endpoints sold one by one; Indian mid-market ACVs are $1-5k/month, meaning 60-100 endpoints are needed for ~$1M ARR and the sales motion, not the tech, is the bottleneck.
- Commoditisation from above: Red Hat (llm-compressor, RHAIIS at ~$2,500/yr per accelerator), NVIDIA (ModelOpt AutoQuantize, free Dynamo/TRT-LLM, pre-quantized NVFP4 checkpoints) and vLLM itself could ship an accuracy-gated auto-recipe and precision headers; our open-core planner would then be a feature of the engine, leaving only the ledger, India capacity and regulated installs.
- Simplismart or Baseten can copy the accuracy card and precision pin in one sprint; they have 58 people, NVIDIA as investor and existing customers. Our only defence is being the reference measurer first and cheaper on Ampere/Ada in India.
- Accuracy SLA liability: customer eval sets are small and noisy (stderr on 200 items is 2-3 pts), graders disagree, and a 1.5-pt threshold will produce disputes; mis-drafted terms could make us liable for model behaviour rather than precision drift. Needs tight legal language (credits capped at monthly fees, precision-drift only) and minimum eval-set sizes.
- India GPU supply and pricing volatility: E2E/Neysa/Jarvislabs on-demand L40S/A100 inventory is thin, prices move with demand, Yotta is aligned with Simplismart, and IndiaAI Mission allotments are bureaucratic; a committed-capacity contract is needed before we can promise 99.9% and we cannot afford it before ~20 endpoints.
- Solo on-call is not credible: a 1-person team cannot honour even a 99.5% SLA across time zones; the contractor SRE hire in month 2-3 is a hard dependency, and an outage during a pilot kills the trust story the product is built on.
- Toolkit churn: llm-compressor/vLLM/compressed-tensors ship breaking changes monthly (ModelOpt changed MoE checkpoint formats in 0.47; NVFP4 KV scales were exported 6x wrong until 0.49; AutoAWQ/AutoGPTQ/quanto died in 2025); the weekly compat-matrix refresh is real engineering cost and a single bad upgrade can invalidate dozens of cards.
- Models going natively low-precision (Gemma 4 QAT, Kimi K3 MXFP4, DeepSeek-V4 FP4) shrink the PTQ value-add; the residual value is serving those formats correctly on Ampere/Ada where kernels are missing (MXFP4 has no Hopper-native path, Marlin fallback on Ampere), which is thinner than quantizing ourselves.
- Speculative-decoding gains vanish at batch >16 and conflict with W4A16 targets (SpecMQuant), so the headline 2-3x applies to low-batch endpoints only; customers who grow into high throughput will find H100 FP8 at Fireworks/Simplismart cheaper per token and churn upward.
- Long-context agent workloads (>=128k) still need H100/H200-class memory because sub-8-bit KV is not production-ready (3-bit loses ~20 pts on reasoning); we cannot right-size those onto L40S and will lose them to incumbents.
- Regulated on-prem deals (banks, hospitals, PSUs) have 6-12 month cycles, need SOC 2/ISO and sometimes CERT-In empanelment, and competitors there are Red Hat, Cohere North, SambaNova racks and AirgapAI; cash runs out before these close unless the managed tier funds the company.
- AMD and spot serving are phase 2 promises: MI300X/MI355X are effectively unavailable in India, ROCm vLLM FP8/MXFP4 paths need per-model validation, and spot replicas add failure modes a tiny team cannot debug while on-boarding customers.
- Precision disclosure cuts both ways: publishing honest GOLD/SILVER grades means some popular recipes (Llama-3.1-8B W4A16, NVFP4 on 7-14B) will be shown failing, and customers may prefer a vendor who does not tell them.


---

## Design [vertical]: Sankshep (संक्षेप, "condensed") — Indic voice inference appliance

**One-liner:** Accuracy-gated, quantized Indic ASR + LLM + TTS stack that runs Indian bank/NBFC/BPO call automation and call-QA on the GPUs Indian data centres actually have (T4/A10G/L4/A100) or on CPU, inside the customer's own perimeter, at under ₹0.30 per call-minute all-in — with a signed per-language Eval Card for every artifact so nobody is running "silently quantized" models on regulated customer calls.

**Target customer:** Primary (first 12 months): the ~25 Indian companies that already sell Indic voice automation and call analytics into BFSI and must now deploy inside the client's VPC/on-prem instead of calling cloud APIs — voice-AI ISVs (Skit.ai, Gnani.ai, Rezo.ai, Ori, Floatbot, Yellow.ai's voice line), CCaaS/CPaaS platforms (Exotel, Ozonetel, Knowlarity/Gupshup, Tata Tele Business Services, Kaleyra) and collections/customer-support BPOs (Startek, Firstsource, iEnergizer, HGS, Conneqt). Buyer: CTO / Head of Platform; CISO signs off. They have the enterprise contracts and the telephony; they lack cheap, auditable on-prem inference. Secondary (via those partners, 2–3 lighthouse deals direct): mid-size NBFCs, small finance banks, insurers and MFIs with 200–3,000 agent seats and heavy Hindi/Tamil/Marathi/Bengali/Telugu/Kannada call volume (Muthoot, Shriram Finance, Ujjivan SFB, Equitas SFB, CreditAccess Grameen, Go Digit, Acko, Piramal Finance) — Head of Collections / Customer Service as champion. Tertiary: state/PSU helplines (104 health, 1912 power, CSC e-Governance) through GeM-listed SIs; government is slow and is a 2027 channel, not a 2026 one. Explicitly not targeting: US customers, image/video gen, frontier-model hosting, hyperscale token resale.

**Problem:** Indian regulated enterprises run hundreds of millions of phone minutes a month in 10+ languages and code-mixed Hinglish/Tanglish, and want AI for three jobs: (1) outbound/inbound voicebots (EMI reminders, KYC, FAQs), (2) agent assist, (3) call QA/compliance monitoring (RBI Fair Practices Code for collections, mis-selling checks). Four constraints make the obvious cloud-API path break: (a) data residency and vendor-risk pressure — DPDP Act 2023 with Rules notified Nov 2025 and phased obligations (verify exact dates), RBI's 2018 payment-data localisation, RBI's IT-outsourcing (2023) and IT-governance directions, and RBI's FREE-AI framework (Aug 2025) pushing banks toward governed, auditable, preferably indigenous models — so CISOs increasingly demand on-prem or Indian-cloud VPC deployment; (b) economics — a human agent costs ₹3–5 per talk-minute, Western voice-agent stacks (ElevenLabs/Vapi-class) ₹7–8/min, Indian API stacks (Sarvam/Google/Azure ASR+TTS+LLM) roughly ₹1.5–3/min blended (verify; Sarvam's published rates were ~₹30/hr ASR and ~₹15 per 10k TTS characters), while collections and support only pay off below ~₹0.5/min; (c) hardware — India had ~34k GPUs (100k target by Dec 2026), enterprise DCs mostly hold T4/A10G/L4/A100-40GB or just Xeons, H100s cost ₹200–400/hr, and FP16 models do not fit useful concurrency on 16–24 GB cards (Llama-3.1-8B FP16 KV alone is 256 MiB per 2k-token call); (d) accuracy risk — INT4 quantization measurably hurts low-resource languages more than English (AWQ-int4 −4.7, GPTQ-int4 −3.8 points on Hindi/Tamil-class languages in EMNLP 2025 work; a 2026 preprint shows structural collapse for non-Latin scripts in edge SLMs), vanilla Whisper and Google STT are near-unusable on rural phone-call Hindi (GramVaani: 59.9% WER for Google STT vs 26.8% for IndicWhisper), and no vendor publishes per-language, per-precision evals or contractual precision disclosure. Result: teams either overpay for cloud APIs, or quantize blindly with archived tools (AutoAWQ/AutoGPTQ) and discover regressions in production on live customer calls. Nobody sells the combination: cheap-GPU/CPU quantized Indic voice stack + domain eval sets + audit-grade evidence.

### Product

## What it is

Sankshep is an open-core, on-prem **Indic voice inference appliance**: a container bundle + a catalog of accuracy-certified quantized models + an evaluation gate, sold to teams that automate or audit Indian-language phone calls. "Quantized" in both senses: the models are INT8/INT4/FP8/GGUF, and the scope is deliberately narrow (4 languages, 1 domain, 3 hardware tiers at launch).

### Layer 1 — Catalog (the paid asset): Indic-calibrated artifacts with signed Eval Cards, per hardware tier
- **ASR**: AI4Bharat IndicConformer-600M hybrid RNNT (MIT, 22 languages; .nemo) exported to ONNX int8 for sherpa-onnx (CPU streaming) and FP16/INT8 TensorRT for GPU batch; IndicWhisper / whisper-large-v3-turbo per-language fine-tunes (MIT) converted to CTranslate2 `int8_float16` (GPU) / `int8` (CPU) for faster-whisper batched decoding; Voxtral-Mini-3B (Apache-2.0, Hindi) as a GPU alternative (verify Indic coverage beyond Hindi); a small language-ID model for auto language routing.
- **LLM**: Sarvam-M 24B and Sarvam 30B (Apache-2.0 per digest), Gemma 4 QAT (E4B / 12B / 26B-A4B) as w4a16 compressed-tensors, a Llama-3.1-8B Indic fine-tune, Qwen3-8B/14B — shipped at FP8 W8A8 + FP8 KV (Ada/Hopper), INT8 W8A8 and W4A16 (Ampere/Turing), and GGUF Q4_K_M/Q8_0 with an Indic imatrix (CPU).
- **TTS**: Kokoro-82M (Apache-2.0; Hindi + English voices) as ONNX int8 for telephony-grade sub-150 ms TTFB; Indic Parler-TTS (AI4Bharat/HF, 21 languages; Apache-2.0 — verify) in BF16/FP16 on GPU for languages Kokoro lacks; IndicF5 excluded until its repo states a license (it currently does not).
- **Aux**: Silero VAD (MIT), a quantized Indic NER/PII redactor (Aadhaar/PAN/phone/amount masking before storage), BGE-M3 int8 embeddings for FAQ-RAG.
- Every artifact ships with an **Eval Card** (signed JSON + PDF): precision/recipe, calibration-set hash and language mix, engine + kernel versions, hardware compatibility, per-language WER / MILU / entity-accuracy / KL-vs-BF16 numbers, date. This is the document a bank's model-risk reviewer actually asks for.

### Layer 2 — Stack (Apache-2.0): `sankshep-stack`
docker-compose and Helm (K3s-friendly) bundle: vLLM (LMDeploy TurboMind on Ampere when INT8 KV is needed); ASR service (FastAPI + WebSocket over sherpa-onnx / CTranslate2, Silero VAD, 8 kHz μ-law/A-law ingest and resampling, word timestamps, entity spans); TTS service (sentence-chunked, 20 ms frame streaming); Pipecat-based pipeline (BSD-2; Exotel, Plivo, Twilio, Telnyx serializers already exist upstream; we add Ozonetel and Asterisk/FreeSWITCH AudioSocket); batch Call-QA worker; gateway (API keys, tenants, append-only audit log, PII redaction, retention policy); Prometheus + Grafana with a ₹/call-minute meter; air-gap installer (`sankshep bundle --airgap` produces images + artifacts + checksums on a tarball/USB).

### Layer 3 — Forge + Gate (Apache-2.0 core; hosted runs are paid)
`sankshep-forge` = quantize → evaluate → sign pipeline (llm-compressor, AutoRound, llama.cpp imatrix, CTranslate2, onnxruntime quantizer, ModelOpt for Blackwell). `sankshep gate run <artifact>` executes the Indic Quant Gate (see quantization strategy) against any model — including a customer's own fine-tune — and emits an Eval Card; also packaged as a GitHub Action ("Indic Quant CI").

## Two modes (UX)
- **Mode A — Call QA / analytics (batch; first revenue).** Recordings land in S3/MinIO/SFTP → diarized, code-mixed transcripts → LLM scoring against the customer's rubric (collections: abuse/threat language, mandatory disclosures, promise-to-pay capture, call-back date/amount extraction; support: resolution, sentiment, script adherence) → dashboard, CSV, webhook. Runs overnight on T4/L4 or CPU. Target ₹0.05–0.15 per audio-minute all-in including amortized hardware. Low latency risk, high audit value, easy pilot.
- **Mode B — Real-time voice agent / agent assist.** Telephony leg → VAD → streaming ASR → LLM with tools (CRM lookup, EMI schedule, OTP flow) → TTS, with barge-in and endpointing. Target p50 turn latency ≤ 1.2 s, p95 ≤ 2.0 s on one L4 for 80–120 concurrent calls (to be measured in week 5). Agent-assist variant streams live transcript + suggested replies + compliance nudges to a human agent's desktop.

## API surface
- `POST /v1/chat/completions`, `/v1/completions`, `/v1/embeddings` — OpenAI-compatible (vLLM passthrough) with hardware-explicit model aliases, e.g. `sankshep/sarvam-m-24b-w4a16-l4`, `sankshep/gemma4-12b-fp8-l4`.
- `WS /v1/audio/stream` — bidirectional: PCM16 8/16 kHz or μ-law in; partial/final transcripts, word timestamps, language id, entity spans (amount, date, phone, PAN-like) out.
- `POST /v1/audio/transcriptions` — Whisper-API-compatible batch endpoint with `diarize=true`, `language=auto|hi|ta|mr|en-IN`.
- `POST /v1/audio/speech` — OpenAI-compatible streaming TTS, `voice=hi_f_1`, `format=mulaw8k|pcm16`.
- `WS /v1/voice/session` — full pipeline bound to a telephony leg; events `user_said`, `bot_said`, `tool_call`, `handoff`, `hangup`; prompt/tool config per campaign.
- `POST /v1/qa/jobs` — batch call QA with rubric id; results via webhook; `GET /v1/qa/jobs/{id}`.
- `GET /v1/models/{id}/eval-card` — signed Eval Card JSON (cosign signature verifiable offline).
- CLI: `sankshep plan --gpu L4 --langs hi,ta --concurrency 120` (chooses artifacts + launch flags, prints VRAM/KV budget and ₹/min), `sankshep gate run`, `sankshep bundle --airgap`, `sankshep bench` (GuideLLM + audio load generator).

## What it is not
Not a general LLM hosting platform, not a token marketplace, not a kernel company, not a chatbot builder. ISVs keep their dialog logic; we are the inference floor underneath it.

### Technical architecture

## Components (all pinned versions, one `sankshep.lock` so toolkit churn is our problem, not the customer's)

| Component | Choice | License | Why |
|---|---|---|---|
| LLM engine | vLLM (compressed-tensors, FP8, Marlin W4A16, GPTQ/exllama for T4, FP8 KV, n-gram spec decode, prefix caching) | Apache-2.0 | Loads llm-compressor artifacts natively; broadest GPU table |
| LLM engine (Ampere alt) | LMDeploy TurboMind | Apache-2.0 | Online INT8/INT4 KV cache on A10G/A100 (head_dim must be 128 — fine for Llama/Sarvam-M, not Gemma) |
| CPU LLM | llama.cpp server (GGUF, Indic imatrix) | MIT | Branch/district offices, air-gapped PoCs, ≤10 concurrent |
| ASR streaming | sherpa-onnx (NeMo transducer ONNX int8, Silero VAD) | Apache-2.0 | CPU/GPU, Python+C++, Android/Jetson later |
| ASR batch | faster-whisper / CTranslate2 (int8_float16) with IndicWhisper + turbo fine-tunes | MIT | Best Hindi WER on Vistaar; batched pipeline ~100x+ real-time on L4 (measure) |
| TTS | Kokoro ONNX int8 (hi/en), Indic Parler-TTS FP16 (other langs) | Apache-2.0 | Real-time on CPU for Kokoro |
| Pipeline | Pipecat (Exotel/Plivo/Twilio serializers upstream; our Ozonetel + Asterisk AudioSocket adapters) | BSD-2 | Telephony plumbing exists; swap in self-hosted services |
| Quantizers | llm-compressor 0.14.x, AutoRound (AutoScheme), llama.cpp imatrix, CTranslate2 converter, onnxruntime dynamic int8, NVIDIA ModelOpt (Blackwell only) | Apache-2.0 / MIT | Maintained paths; AutoAWQ/AutoGPTQ are archived |
| Eval | lm-evaluation-harness (custom YAML tasks: MILU subsets, IndicXTREME, domain intent/slot), jiwer (WER/CER), our entity-error harness, GuideLLM, custom audio load generator | MIT / Apache-2.0 | Reproducible by third parties |
| Gateway/ops | FastAPI gateway, Postgres (audit, jobs), MinIO (recordings, optional), Prometheus + Grafana, cosign for artifact signing, Helm + K3s, docker-compose for single-node | — | Boring on purpose |

## Data flow (Mode B, real-time)
```
PSTN/SIP (Exotel|Ozonetel|Asterisk) --8kHz mulaw--> Pipecat transport
  -> Silero VAD (CPU) -> ASR svc (sherpa-onnx int8 | faster-whisper int8_float16, 8->16kHz resample)
  -> partials/finals + entities -> Orchestrator (prompt, tools, state; PII redaction before log)
  -> vLLM (W4A16/FP8 Indic LLM, FP8 KV, prefix-cached system prompt, n-gram speculative)
  -> sentence chunker -> TTS svc (Kokoro int8 | Parler FP16) -> 20ms frames -> transport
  -> barge-in: VAD speech-start cancels TTS + LLM stream
Audit: every turn -> Postgres (redacted), metrics -> Prometheus (TTFT, ASR final latency, TTS TTFB, turn latency, ₹/min)
```
Mode A (batch QA): recordings → queue → diarization (pyannote or sherpa-onnx speaker embeddings) → batched ASR → chunked LLM scoring (24–30B at W4A16/FP8) → rubric JSON → dashboard/webhook. No latency constraint, so it runs on T4s or CPUs overnight.

## Latency budget (target, one L4, 100 concurrent calls)
VAD endpoint 200–300 ms → ASR final 100–200 ms (streaming conformer) → LLM TTFT ≤ 300 ms (8B W4A16; prefix-cached system prompt, ~150 new tokens prefill) → first sentence (~15 tokens at ≥20 tok/s/call) ~450 ms → TTS TTFB ≤ 150 ms ⇒ ~1.0–1.2 s p50. Hindi needs 7–8 tok/s per call for real-time speech on Llama-3 tokenizers (3 tokens/word); Sarvam/Gemma tokenizers need less.

## Why KV quantization matters here (the 24 GB card math)
- Llama-3.1-8B: 32 layers × 8 KV heads × 128 dim × 2 (K,V) × 2 B = 128 KiB/token → 256 MiB per 2k-token call at FP16; 128 MiB at FP8. W4A16 weights ≈ 5.5 GB. On a 24 GB L4 with ~2 GB activations: ~60 concurrent calls at FP16 KV, ~120 at FP8 KV. FP16 weights (16 GB) leave room for ~20 calls — this is why FP16 "default" is dead on Indian hardware.
- Sarvam-M 24B (40 layers, 8 KV heads, 128 dim): 160 KiB/token → 320 MiB per call; W4A16 ≈ 13 GB → ~28 calls at FP16 KV, ~55 at FP8 KV on L4; 24B is the agent-assist/QA model, 8–12B the voicebot model.
- Gemma head_dim = 256 doubles KV per token and the vLLM FP8-KV study shows worse TTFT scaling for head_dim-256; Gemma's sliding-window layers must be skipped (`--kv-cache-dtype-skip-layers sliding_window`).
- Decode throughput on L4 (300 GB/s): batch-64 step reads ~5.5 GB weights + ~8 GB FP8 KV ≈ 45 ms → ~1,400 tok/s aggregate, ~22 tok/s per call — 3x real-time speech. A voicebot fleet needs ~5–10 tok/s per active call, so one L4 ≈ 80–120 calls LLM-side, KV-bound not compute-bound.

## Hardware tiers and recipes
| Tier | GPU (India on-demand) | LLM recipe | KV | ASR | Est. concurrent calls/node (measure W5) |
|---|---|---|---|---|---|
| CPU-only | 32-vCPU Xeon (AMX) / EPYC, ₹5–8k/mo | GGUF Q4_K_M / Q8_0 (Indic imatrix), Gemma 4 QAT Q4_0, ≤4B for real-time | FP16 | sherpa-onnx int8 conformer | 5–10 real-time; batch QA at ~20–40x real-time |
| Turing | T4 16 GB (~₹0.53/hr AWS g4dn, Simplismart lists $1.20) | W4A16 GPTQ (exllama kernels; no Marlin, no FP8), ≤9B | FP16 (e5m2 to validate) | CTranslate2 int8_float16 | 30–40 |
| Ampere | A10G 24 GB (~$1/hr g5), A100-80 (₹189/hr E2E) | W8A8 INT8 (SmoothQuant+GPTQ) for speed, W4A16 Marlin for fit; no FP8 GEMM | LMDeploy INT8 KV or vLLM fp8_e5m2 (validate) | CTranslate2 int8_float16 | 60–100 (A10G) |
| Ada | L4 24 GB (₹49/hr E2E), L40S 48 GB ($1.20/hr) | FP8 W8A8 dynamic for 8–12B (lossless), W4A16 for 24–32B; W4A8 (QServe-class) on L40S later | FP8 calibrated | CTranslate2 int8_float16 | 80–120 (L4), 150–250 (L40S) |
| Hopper | H100 (₹379/hr) | FP8 + FP8 KV, EAGLE-3 only on FP8 targets, 70B-class for QA/summarization | FP8 | NeMo TensorRT FP16/INT8 | 300+ |
| Blackwell | B200/RTX PRO 6000 (Yotta, rare) | NVFP4 via ModelOpt/llm-compressor | NVFP4/FP8 | — | 2027 item |

## Deployment shapes
Single-node docker-compose (pilot: 1× L4 or 1× A10G + 16 vCPU); Helm on K3s/EKS-Mumbai/E2E-Kubernetes for 3–10 nodes; air-gapped tarball with offline images, artifacts, cosign public key, and a one-page validation runbook. Upgrades = new artifact + new Eval Card; engine version pinned per release; rollback by alias.

### Quantization strategy

## Principles
1. Precision is chosen per (model, GPU generation, language set, SLO), never globally; the default is the **least** aggressive precision that hits the concurrency target on the customer's hardware.
2. Every artifact passes an **accuracy gate measured per language**, not on an English average.
3. We quantize the whole voice path (ASR, LLM, KV cache, TTS, NER), because on a 24 GB card the LLM is only one of three memory consumers.
4. We publish the precision and the numbers. Precision disclosure is a feature regulated buyers will pay for.

## Methods by component
**LLM weights**
- Ada/Hopper: FP8 W8A8 dynamic per-token (`QuantizationModifier(scheme="FP8_DYNAMIC")`, llm-compressor). Evidence: effectively lossless at 8B–405B (ACL 2025, 99.75% recovery). This is the default for 8–12B voicebot models on L4/L40S.
- Ampere/Turing: W8A8 INT8 (SmoothQuant α=0.5–0.8 + GPTQ, `ignore=["lm_head"]`) when the model fits — Red Hat measured L40S 576→830 tok/s and accuracy deltas within std-error on Llama-3.1-8B; W4A16 GPTQ/AWQ g128 (Marlin on SM80+, exllama on T4) when it does not (24B on A10G). Expected recovery ~99% on English; our job is to measure and recover it on Indic.
- CPU: llama.cpp Q4_K_M / Q5_K_M / Q8_0 with an **Indic imatrix** (`llama-imatrix` on our calibration corpus, not English wikitext); Gemma 4 official QAT Q4_0 where available.
- Sub-4-bit (W2/W3 via AutoRound, AQLM/VPTQ): research track only; no production kernels upstream and small models collapse (AQLM 2-bit Llama-3.2-3B MMLU 0.60→0.48). Not shipped.
- Blackwell NVFP4 via ModelOpt/llm-compressor only when a customer actually has SM100; on Hopper NVFP4 is a Marlin W4A16 fallback with no speed gain, so we do not bother.

**Mixed precision / sensitive layers (hypotheses to test in week 2, then baked into recipes)**
- Keep embeddings and `lm_head` in BF16 for Indic (large vocabularies: Gemma 262k, Sarvam expanded tokenizer); test whether the first 2 and last 2 decoder blocks and attention `o_proj` need 8-bit when the rest is 4-bit.
- Use llm-compressor HIGGS (ILP under a bits-per-weight budget) and AutoRound AutoScheme to search per-layer bits at ~4.6–5.0 bpw with the gate as the objective; report the final effective bpw on the Eval Card.

**Calibration (our most important hypothesis)**
- `IndicCalib-v1`: 1,024 samples × 2,048 tokens, chat-templated, `add_special_tokens=False`: 35% Hindi + Hinglish conversational (IndicAlign-style SFT data, Sangraha web text filtered for conversation, our synthetic BFSI dialogues), 15% Tamil, 10% Marathi, 10% Bengali/Telugu/Kannada mix, 15% Indian English, 10% JSON tool-call traces, 5% numeral-heavy text (amounts, dates, OTP readback). Published hash goes on every Eval Card.
- Hypothesis H1: Indic-matched calibration recovers at least half of the documented −3.8 to −4.7 pt "Indic INT4 tax" versus English-calibrated GPTQ/AWQ. If true, it is our first public benchmark post; if false, mixed precision carries the load and we say so. The ScaleQ-1.58 finding (accuracy still rising at 16M calibration tokens) suggests calibration volume matters more than people assume, so week 2 also sweeps 256 → 1,024 → 4,096 samples.

**KV cache**
- Ada/Hopper: FP8 KV with calibrated per-head scales from llm-compressor (`kv_cache_scheme` num_bits 8, float, static) → vLLM `--kv-cache-dtype fp8`; skip sliding-window layers on Gemma. Doubles concurrent calls on L4; break-even for per-token decode cost is ~7k tokens, but our constraint is capacity, not per-token speed, so it pays off at 2k-token calls.
- Ampere: LMDeploy TurboMind online INT8 KV (head_dim 128 models), or vLLM fp8_e5m2 if validated on A10G in week 5.
- Sub-8-bit KV (TurboQuant 3–4-bit, KIVI 2-bit): not for the real-time path — vLLM's own study shows ~20-pt reasoning losses at 3-bit and 66–80% throughput; maybe for batch QA of very long calls later.

**ASR**
- NeMo IndicConformer-600M RNNT → ONNX → onnxruntime dynamic int8 (sherpa-onnx), chunked streaming with lookahead; GPU: FP16 TensorRT, INT8 only if WER gate passes.
- Whisper-family (IndicWhisper, turbo fine-tunes) → CTranslate2 `int8_float16` (GPU) / `int8` (CPU); batched decoding with VAD-segmented inputs; guard against quantized-Whisper hallucination: VAD gating, no temperature fallback, compression-ratio and no-speech thresholds, hallucination rate measured on silence/noise segments.
- Telephony reality: 8 kHz μ-law upsampled to 16 kHz; fine-tune (not just quantize) on 8 kHz-bandlimited augmentation of Kathbath/IndicVoices + GramVaani; quantization delta is only meaningful once the base model is usable on this audio.

**TTS**: Kokoro-82M ONNX int8 (CPU real-time); Parler-TTS FP16 with static batching; measure, do not assume, that int8 helps Parler (TTS is the least studied; FP16 + batching may be the honest answer for GPU TTS).

**Speculative decoding**: vLLM n-gram/prompt-lookup speculation on the voicebot path (templated phrases repeat; safe with W4A16 targets). No EAGLE on INT4 targets (SpecMQuant: tree verification erases the memory-bound win). EAGLE-3 only on FP8 targets at batch ≤ 8 (agent assist).

**Reasoning models**: not on the real-time path (latency, token inflation under quantization); QA scoring uses non-thinking 24–30B models.

## The Indic Quant Gate (promotion criteria vs. BF16/FP16 reference on the same hardware)
LLM artifact promoted only if ALL hold, per target language (hi, hinglish, ta, en-IN at launch; mr, bn, te, kn next):
1. MILU per-language subset (lm-eval custom task) recovery ≥ 98.5% (each language, not average); IndicXTREME/IndicGenBench spot checks ≥ 98%.
2. Domain set (2k human-verified BFSI/support dialogues): intent accuracy drop ≤ 0.5 pt; slot/entity F1 (amount, date, EMI, last-4 digits) drop ≤ 0.5 pt; JSON tool-call validity ≥ 99.5%.
3. Token-level KL divergence vs BF16 on 2k Indic/Hinglish prompts: mean ≤ 0.02, p99 ≤ 0.5 (Unsloth-style thresholds, our own calibration of the limits in week 2).
4. Script-integrity rate (mojibake, wrong-script output, repetition collapse detected by script detector + regex) ≤ 0.1% of responses — the documented failure mode for non-Latin scripts.
5. Long-context: 8–16k-token call-summary judge score drop ≤ 2%; needle test unchanged when FP8 KV is on.
6. Efficiency: ≥ 1.5x concurrent calls per GPU vs the reference, else it is not shipped.
ASR gate: WER delta ≤ +0.5 abs per language and per dataset (Kathbath, Kathbath-Hard, GramVaani, Svarah, our 8 kHz set); entity error rate (digits/amounts/dates/names) delta ≤ +0.3; hallucination on non-speech ≤ 0.5% of segments; streaming RTF < 0.3 on the target CPU/GPU.
TTS gate: ASR round-trip WER delta ≤ +0.5; UTMOS drop ≤ 0.05; numeric/currency/date pronunciation suite ≥ 99% pass.
All of it runs in `sankshep gate` with GuideLLM load profiles (constant, poisson, sweep) so the Eval Card carries both accuracy and TTFT/ITL/throughput for the stated hardware.

## Evidence we build and publish
- "The Indic INT4 tax, measured": 6 models × 4 precisions × 4 languages × 3 GPUs, open harness, reproducible.
- Public "Indic Quant Index" leaderboard of our and others' artifacts (Sarvam, Unsloth, RedHatAI, Google QAT) under the same gate — community pull and sales collateral at once.

Verification note: GramVaani being 8 kHz telephony, Sarvam API prices, Indic Parler-TTS and Voxtral details, and DPDP/FREE-AI specifics are from memory (search budget exhausted during this task) and are marked "(verify)" where used; IndicConformer (MIT, 600M RNNT), Vistaar/IndicWhisper (MIT; Hindi 13.6% avg, GramVaani 26.8% vs Google 59.9%), sherpa-onnx (Apache-2.0, NeMo transducer int8, Silero VAD, streaming) and Pipecat (BSD-2, Exotel serializer) were confirmed from primary pages today.

### Differentiation vs Simplismart

Simplismart is a horizontal, closed, US-majority-revenue GenAI serving platform (LLM, Whisper, diffusion, video) whose thesis is "fewer GPUs per workload" via 28 custom CUDA kernels and a Terraform-like control plane; quantization there is a config knob (FP16 default; FP16/BF16/FP8/AWQ/GPTQ; FP8 explicitly unsupported on A100/A10G), benchmarks are single-user H100 tok/s, and it prices GPU-hours at roughly E2E's raw rate ($4/hr H100). Sankshep differs on seven concrete axes: (1) Scope — one vertical (Indic voice + LLM for Indian regulated call operations) instead of every modality for everyone; we ship telephony plumbing (8 kHz μ-law, Exotel/Ozonetel/Asterisk), diarization, PII redaction and QA rubrics that Simplismart will never prioritise. (2) Hardware — we optimise for the T4/A10G/L4/A100/CPU tier Indian enterprises own, with validated INT8/W4A16/INT8-KV recipes where Simplismart's FP8 story stops; they win on H100 throughput and we do not pretend otherwise. (3) Quantization as product — accuracy-gated, per-language, mixed-precision, KV-cache and ASR/TTS quantization with Indic-calibrated artifacts, versus their FP16-default with three formats; they have nothing public on KV-cache sub-8-bit, QAT, GGUF/ONNX int8 for CPU, or automatic accuracy-guarded search. (4) Evidence — they publish vendor tok/s; we publish WER/MILU/entity-accuracy per language per precision from an open, third-party-reproducible harness, and sign it. Their Sanas INT4 case ("99.99% accuracy retention") is bespoke services; ours is productised CI. (5) Openness — Apache-2.0 stack and gate, paid artifacts/support, so Indian developers can pull it like vLLM; Simplismart has zero open-source surface and zero community pull. (6) Commercial model — ₹ per concurrent channel or per node, plus per-release certification, mapped to call-centre budgets, not $/M tokens or GPU-hour resale at zero markup. (7) Regulatory posture — Eval Cards and validation runbooks written for RBI FREE-AI / DPDP model-governance reviews; Simplismart sells "BYOC/air-gapped" as a deployment mode, not a compliance artifact. Honest caveat: Simplismart has $21M, NVIDIA as investor and partner, 58 people, Yotta as a channel, and could add Indic evals in a quarter; our bet is that they will not go down-market into ₹0.30/min telephony on T4s because their US video-gen customers pay more. They are as plausible an acquirer or partner as a competitor.

### Moat

Thin for the first 12 months and I will not dress it up; algorithms and kernels are commoditised by Red Hat, NVIDIA, Intel and Google. What compounds: (1) BharatVoiceEval — consented, 8 kHz, noisy, code-mixed, entity-labelled telephony test sets and calibration packs per language and domain (collections, KYC, support), built with annotators (Karya/Desicrew-class) and extended with every pilot's agreed synthetic/consented samples; this is expensive to assemble, cheap to reuse, and nobody has it (not Sarvam, not Simplismart, not Unsloth). (2) Validated recipe matrix — (model × GPU generation × language set × SLO) recipes that passed the gate, with the failure knowledge (which layers, which scripts, which Whisper hallucination settings) encoded in Forge; individually trivial, in aggregate months of GPU-hours. (3) Compliance artifacts and auditor relationships — Eval Cards and validation runbooks that bank model-risk teams and their auditors have accepted once become the path of least resistance for the next vendor; precision disclosure as a contractual term is a category we can define. (4) Distribution lock-in — embedded in CCaaS/ISV stacks via the pipeline adapters and `sankshep plan` sizing; once a bot fleet is sized to our artifacts and the audit trail references our Eval Cards, swapping is a re-validation project. (5) Open-core community in India — the gate and stack as the default way Indian developers test quantized Indic models (the "Indic Quant Index" leaderboard). What is NOT a moat: kernels, FP8/INT4 itself, vLLM integration, the Pipecat pipeline. Exit logic is honest too: compression-tool revenue is small even for public companies (Nota ~$5.9M), so the realistic outcomes are a profitable ₹10–30 Cr/yr vertical business or acquisition by an Indian cloud (Yotta/E2E/Neysa), a CCaaS platform, Sarvam, or Simplismart itself.

### 8-week MVP

## Team assumption: founder-engineer (serving + quant + sales), 1 speech/ML engineer, annotation outsourced. Languages at launch: Hindi, Hinglish, Tamil, Indian English. Domain: BFSI collections + support.

**Week 1 — Baselines and harness v0**
- Repo skeleton: `sankshep-forge`, `sankshep-stack`, `sankshep-gate`; pinned `sankshep.lock` (vLLM, llm-compressor 0.14.x, AutoRound, CTranslate2, sherpa-onnx, lm-eval 0.4.13, GuideLLM).
- lm-eval custom YAML tasks: MILU per-language subsets, IndicXTREME spot tasks; jiwer WER/CER harness; entity-error-rate scorer (digits, amounts, dates, names) for ASR and slot F1 for LLM.
- BF16/FP16 references on A100-80 (E2E): Sarvam-M 24B, Gemma 4 12B, Llama-3.1-8B Indic FT, Qwen3-8B; IndicConformer-600M and IndicWhisper on Kathbath, Kathbath-Hard, GramVaani, Svarah.
- Commission annotation: 30 hours of 8 kHz-style collections/support audio across 3 languages (synthetic scripts read by voice actors + consented role-play), transcripts + entity tags; 2,000 BFSI dialogues generated with a large model, human-verified. Deliverable: baseline table, data orders placed.

**Week 2 — LLM quantization sweep + H1 test**
- llm-compressor recipes: FP8_DYNAMIC (L4/H100), INT8 W8A8 SmoothQuant+GPTQ, W4A16 GPTQ g128 and AWQ g128 (Marlin), each with English (ultrachat) vs `IndicCalib-v1` calibration, 256/1,024/4,096 samples; lm_head/embeddings BF16 variants; AutoRound AutoScheme at 4.6 bpw.
- Run the gate on all variants × 4 languages; compute KL vs BF16; script-integrity scan. Deliverable: first recipe matrix and the H1 result (does Indic calibration recover the INT4 tax?). Pick the voicebot model (8–12B) and the QA model (24–30B).

**Week 3 — ASR and TTS quantization**
- IndicConformer → ONNX → onnxruntime int8 → sherpa-onnx streaming (CPU 8-vCPU and L4); IndicWhisper / turbo fine-tune → CTranslate2 int8_float16 batched; WER/entity/hallucination gate on all five datasets; RTF and concurrency per core/GPU.
- 8 kHz band-limiting augmentation fine-tune of the chosen ASR model (light, 1–2 days on A100) — quantization is pointless if the base model cannot hear telephony.
- Kokoro ONNX int8 Hindi/English TTFB and ASR round-trip; Parler-TTS FP16 batching for Tamil. Deliverable: ASR/TTS artifacts with Eval Cards v0.

**Week 4 — Stack v0 and Mode A (Call QA)**
- docker-compose: vLLM + ASR svc + TTS svc + gateway + Postgres + Prometheus/Grafana; OpenAI-compatible endpoints with hardware aliases; `WS /v1/audio/stream`.
- Batch QA worker: diarization, batched ASR, LLM rubric scoring (collections Fair-Practices rubric + support rubric), CSV/webhook output, ₹/min meter. Deliverable: Mode A end-to-end on 1× L4 and on CPU-only; first internal cost numbers.

**Week 5 — Load, concurrency, cost truth**
- GuideLLM sweeps for the LLM artifacts on L4, A10G (g5.xlarge), T4 (g4dn.xlarge), A100; audio load generator for 50/100/200 concurrent 8 kHz streams; FP8 KV (calibrated scales) on L4 vs FP16 KV; LMDeploy INT8 KV vs vLLM fp8_e5m2 on A10G; n-gram speculative decoding on/off.
- Publish the concurrency-per-node and ₹/call-minute table (replacing the estimates in the architecture). Deliverable: `sankshep plan` sizing CLI backed by measured numbers.

**Week 6 — Gate, signing, public artifacts**
- `sankshep gate run` CLI and GitHub Action; Eval Card schema (JSON + PDF), cosign signing, `GET /v1/models/{id}/eval-card`.
- Push 8–12 artifacts to Hugging Face under `sankshep/` with Eval Cards; publish "The Indic INT4 tax, measured" post with the open harness and the H1 result; launch the Indic Quant Index page. Deliverable: public credibility asset; inbound starts.

**Week 7 — Mode B pipeline and pilot integrations**
- Pipecat pipeline with Exotel serializer (upstream) and an Ozonetel adapter; barge-in, endpointing, tool calls (mock CRM, EMI schedule); demo bot: Hindi/Tamil EMI reminder with amount/date confirmation and promise-to-pay capture; agent-assist web panel (live transcript + suggestions).
- PII redaction (quantized Indic NER + regex for PAN/Aadhaar/phone), audit log, retention policy, DPDP-oriented data-handling one-pager and a model-validation runbook draft. Deliverable: pilot-ready Mode A + demo-ready Mode B; 2 design partners (1 CCaaS/ISV, 1 BPO) start on their sandbox.

**Week 8 — Harden, package, sell**
- Helm chart (K3s), air-gap bundle, upgrade/rollback by alias, license keys; pilot report template (measured WER/accuracy/latency/₹ per minute on partner hardware); pricing sheet; outbound to the 10 target accounts; apply to IndiaAI Mission compute and NVIDIA Inception.
- Deliverable at day 56: open stack on GitHub, 8–12 signed artifacts, public benchmark, Mode A in 2 pilots, Mode B demo on a real phone line, measured economics.

What will slip if only one person: Mode B (week 7) becomes a demo video instead of a live pilot; Tamil TTS waits; Ozonetel adapter waits for a partner ask. Mode A + the gate + the public benchmark are the non-negotiable 8-week outputs.

### GTM

Positioning: "Run Indic call AI on your own hardware at under ₹0.30 a minute — with the eval card your auditor asks for." Sequence: (1) credibility via open artifacts + the "Indic INT4 tax" benchmark (week 6) and the Indic Quant Index; (2) paid pilots on Mode A (call QA) because it is batch, audit-driven and does not risk live customer calls; (3) expand to Mode B voicebots/agent assist inside the same accounts; (4) partner channels.

First 10 to call (named as hypotheses; each has a concrete reason): 1. Exotel (CCaaS; Pipecat serializer already exists → fastest Mode B integration; they sell into BFSI). 2. Ozonetel (CCaaS; strong in collections dialers; needs on-prem AI for bank clients). 3. Skit.ai (voice-AI for collections; must deploy in client VPCs; buy inference floor, keep their dialog IP). 4. Gnani.ai (Indic voice ISV; competitor on models but potential buyer of the gate/eval cards and cheap serving). 5. Rezo.ai or Ori (contact-centre AI ISVs with NBFC logos). 6. Startek India (BPO; call QA on millions of minutes; cost per minute is the whole business). 7. Firstsource or iEnergizer (BPO; collections QA and agent assist). 8. CreditAccess Grameen or Muthoot Finance (lighthouse NBFC/MFI; Kannada/Tamil/Hindi field and phone collections; direct Mode A pilot). 9. Ujjivan SFB or Equitas SFB (small finance bank; CISO-driven on-prem need; agent-assist in branches). 10. Yotta / E2E / Neysa (sovereign-cloud marketplaces: a "Sankshep on L4" SKU; note Yotta already uses Simplismart, so lead with E2E/Neysa). Also seed with 3–5 open-source users (Indic developers on HF) for community signal.

Pricing (INR, designed to capture ~20–30% of the savings vs cloud APIs): Pilot — ₹3–5 lakh fixed, 8 weeks, on their hardware or our E2E L4, includes a measured pilot report. Mode A (call QA) — ₹0.10/audio-minute metered when we host on Indian cloud, or ₹6–8 lakh per node per year on-prem (unlimited minutes on that node, artifacts + Eval Card updates + support). Mode B — ₹2,000 per concurrent voice channel per month, minimum 50 channels (₹1 lakh/month), i.e. ~₹0.10–0.15/min at normal utilisation; enterprise air-gapped tier ₹10–12 lakh per node per year. Gate/certification as a service — ₹1.5–3 lakh per model release for ISVs bringing their own fine-tunes (Eval Card + validation runbook). Reference math for a 200-channel collections deployment: ~3M minutes/month; cloud APIs ₹45–90 lakh/month; Sankshep ₹4 lakh/month licence + ~₹1.5 lakh/month of L4s on E2E (or ~₹8 lakh one-time for 3 L4 cards); human agents for the same minutes ₹90 lakh–1.5 Cr.

Channels: CCaaS/ISV resellers (20–30% margin), GeM listing for government in 2027, E2E/Neysa marketplace SKUs, SI partners for banks (mid-size SIs with RBI-regulated accounts). Content and community: the benchmark post, HF artifacts, talks at IndiaAI/Bhashini/AI4Bharat events, a monthly "Indic Quant Index" update, a free `sankshep gate` GitHub Action. Sales motion: founder-led for the first 10 accounts; 60–90-day pilot-to-annual conversion target; 3 annual contracts by month 9 (~₹40–60 lakh ARR), 10 by month 18 (~₹2–3 Cr ARR). Regulatory framing is a door-opener, not a product: we provide validation evidence, we do not give legal advice.

### Team and cost

Team for the 8-week MVP: (1) Founder-engineer — serving stack, quantization recipes, gate, sales; (2) Speech/ML engineer (₹1.5–2.5 lakh/month, Bengaluru/Chennai mid-senior) — ASR/TTS export and quantization, fine-tuning on 8 kHz audio, eval harness; (3) optional 0.5 FTE DevOps/telephony contractor (₹1–1.5 lakh for the period) for Helm/air-gap and the Asterisk/Ozonetel adapters; annotation outsourced (Karya/Desicrew-class vendors or managed freelancers). Compute for 8 weeks (India on-demand rates from the digest): L4 at ₹49/hr × ~400 h ≈ ₹20k; A100-80 at ₹189/hr × ~120 h ≈ ₹23k (24–30B references and quantization); H100 at ₹379/hr × ~30 h ≈ ₹11k (FP8 references, EAGLE checks); A10G (g5.xlarge ~$1/hr) and T4 (g4dn ~$0.53/hr) on AWS Mumbai ~₹8k; 32-vCPU CPU box ~₹5k; storage/egress ~₹5k → ~₹0.7–1 lakh. Data: 30 audio-hours × 3 languages of transcription + entity tagging at ~₹1,500–3,000 per audio-hour ≈ ₹1.5–3 lakh; synthetic dialogue generation API spend ~₹25k; human verification of 2k dialogues ~₹50k → ₹2.5–4 lakh. Total 8-week cash: ₹7–11 lakh (~$8–13k) with the founder unpaid; ₹11–16 lakh with a founder salary. 12-month run-rate: 3 people ₹60–80 lakh, compute ₹8–12 lakh (more if we host pilots), data ₹10–15 lakh, sales/travel ₹5 lakh, security/compliance basics (VAPT, ISO 27001 prep that bank vendor onboarding asks for) ₹5–10 lakh → ₹1.0–1.3 Cr (~$120–160k). Financing: bootstrap via 3–5 pilots (₹10–20 lakh) plus a ₹3–5 Cr (~$400–600k) pre-seed for 18 months; apply for IndiaAI Mission subsidised compute (₹67–92/GPU-hr for eligible startups), NVIDIA Inception, AWS Activate/Google for Startups credits. Hiring order after seed: a telephony/CCaaS integration engineer, then a sales engineer who has sold into NBFC collections — not more ML researchers.

### Why now

Five things converged in the last 18 months. (1) Indic open models crossed the usable line: Sarvam-M 24B and Sarvam 30B/105B under Apache-2.0, Gemma 4 QAT checkpoints with Indic coverage (Jun 2026), AI4Bharat's IndicConformer (MIT, 22 languages) and IndicVoices data, Voxtral and Meta's Omnilingual ASR — so an on-prem Indic stack no longer depends on a closed API. (2) Quantization tooling consolidated and became free: AutoAWQ/AutoGPTQ died, llm-compressor + AutoRound + ModelOpt own the algorithms, vLLM loads them natively, FP8 KV and INT8 W8A8 are proven lossless-ish, and the evidence that INT4 taxes low-resource languages (−3.8 to −4.7 pts) is published but nobody has operationalised the fix — the algorithm layer is commoditised exactly when the evaluation layer is unowned. (3) Regulation hardened: DPDP Rules notified (Nov 2025, phased), RBI's FREE-AI framework (Aug 2025) and its IT-outsourcing/governance directions put model validation and vendor risk on bank boards' agenda, and 'silent quantization' became a named governance concern in 2026 — precision disclosure is now sellable. (4) Hardware economics in India favour cheap cards: ~34k GPUs nationally, L4 at ₹49/hr, A100 at ₹189/hr, H100 at ₹379/hr, IndiaAI subsidy limited to eligible users; enterprises own T4/A10G/L4/A100 fleets and CPUs, and FP16 serving cannot deliver call-centre concurrency on them. (5) The market just got validated and the gap just got visible: Simplismart's $14M Series B today (NVIDIA, DVC, Accel) proves investors fund Indian inference infrastructure, yet Simplismart is US-majority, closed, H100-first and silent on Indic evals, KV quantization, QAT and CPU — while Kompact AI's CPU-serving claims drew scrutiny precisely because they were unmeasured. A small team that publishes measured, signed, per-language numbers on cheap hardware can own that credibility niche before the incumbents bother.

### Risks

- Base-model quality, not quantization, is the binding constraint on 8 kHz telephony Indic ASR (IndicWhisper is still 26.8% WER on GramVaani; code-mixed Hinglish is worse); if fine-tuning cannot get usable WER, the whole voice pitch stalls regardless of precision.
- H1 may fail: Indic-matched calibration might not recover the INT4 tax, leaving only mixed precision or INT8 — which still works on L4/A100 but weakens the 24 GB-card story for 24B models.
- Sarvam (₹1,500 Cr+ raised, 4,096 subsidised H100s, Apache-2.0 models, existing enterprise on-prem offers) or Google/Azure Mumbai VPC offerings could bundle on-prem Indic voice stacks and make our serving layer a feature; our survival depends on the gate/eval assets, not on serving.
- Full-stack Indic voice ISVs (Gnani, Skit, Yellow.ai) may see us as a competitor rather than a supplier and refuse to adopt; if ISVs do not buy, direct BFSI sales cycles of 6–12 months with vendor-empanelment and infosec audits exceed a small team's runway.
- Data-residency urgency may be weaker than assumed: many banks already accept AWS/Azure Mumbai VPCs, and DPDP Rules obligations phase in over ~18 months (verify), so 'must be on-prem' is a narrower segment than 'wants cheaper'.
- W4A16 buys memory, not speed, on high-end GPUs (Red Hat data); if a customer has H100s or gets IndiaAI-subsidised GPUs at ₹67–92/hr, our cost advantage shrinks to KV-cache and ops value.
- Simplismart, Pruna, Multiverse or Red Hat could ship Indic eval cards in a quarter; our moat is the dataset and auditor acceptance, which take longer to build than to copy once shown.
- Model and data licensing: IndicF5 has no stated license, Indic Parler-TTS/Voxtral/IndicVoices terms need verification, Sarvam model licenses can change; a license surprise can remove a flagship artifact overnight.
- Toolkit churn (AutoAWQ/AutoGPTQ archived, TorchAO in maintenance, vLLM weekly breaking changes) makes the pinned lockfile a permanent maintenance tax on a 1–3 person team.
- Quantized Whisper-class models hallucinate on silence/noise; a hallucinated amount or date on a collections call is a compliance incident, so the ASR gate must be stricter than WER and we may be forced onto larger FP16 ASR models on GPU.
- Speculative decoding and INT4 conflict (EAGLE gains vanish on W4A16 targets), so per-call latency on T4/A10G is bounded by memory bandwidth; sub-1 s turn latency may not be reachable on Turing cards.
- Exit size: compression-tool companies earn little (Nota ~$5.9M revenue at a ~$462M IPO; Pruna ~$2.8M), so the realistic outcome is a profitable niche business or a small acquisition, not a Simplismart-scale raise; investors must be chosen accordingly.
- Solo-founder bandwidth: serving, quantization, evals, telephony integration and enterprise sales are four jobs; without the second engineer by week 2 the 8-week plan slips to 14+ weeks.
- Several Indic-specific numbers in this plan (Sarvam API prices, DPDP Rules dates, RBI FREE-AI details, GramVaani sample rate, some licenses) could not be verified today because the search budget was exhausted; they must be re-checked before going into any customer deck.
