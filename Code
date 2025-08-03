import numpy as np
import math
import time

S0 = 25.66
vol = 0.30
r = 0.06
q = 0.00
T_days = 248
trade_days = np.array([66, 94, 104, 126, 147, 168, 184, 204, 227, 248])
kout_bar = np.array([1.000, 0.995, 0.990, 0.985, 0.980, 0.975, 0.970, 0.965, 0.960, 0.955]) * S0
kin_bar = 0.75 * S0
coupon_out = 0.14
coupon_reb = 0.14
p_call = 0.0
k_call = S0
p_put = 1.0
k_put = S0
bottom = 0.80 * S0
cpn_back = 0.02
prem_back = 0.01 * S0
margin_rt = 0.25
margin_r = 0.03
N_PATHS = 20000
SEED = 42
dt = 1 / 248
n_steps = 248

def pv_one_path(S):
    knock_in = np.any(S <= kin_bar)
    knock_out = False
    tau = n_steps
    for idx, obs in enumerate(trade_days):
        if S[obs] >= kout_bar[idx]:
            knock_out = True
            tau = obs
            break
    df = math.exp(-r * tau / 365)
    if knock_out:
        coup = S0 * coupon_out * tau / 365
        call_pay = p_call * max(S[tau] - k_call, 0)
        cpn_b = S0 * cpn_back * tau / 365
        margin_cost = margin_rt * S0 * margin_r * tau / 365
        return df * (coup + call_pay + cpn_b + prem_back - margin_cost)
    if not knock_in:
        rebate = S0 * coupon_reb * n_steps / 365
        cpn_b = S0 * cpn_back * n_steps / 365
        margin_cost = margin_rt * S0 * margin_r * n_steps / 365
        return df * (rebate + cpn_b + prem_back - margin_cost)
    put_pay = -p_put * min(max(k_put - S[-1], 0), k_put - bottom)
    cpn_b = S0 * cpn_back * n_steps / 365
    margin_cost = margin_rt * S0 * margin_r * n_steps / 365
    return math.exp(-r * n_steps / 365) * (put_pay + cpn_b + prem_back - margin_cost)

def price_and_greeks():
    dS = 0.01 * S0
    np.random.seed(SEED)
    Z = np.random.standard_normal((N_PATHS, n_steps))
    starts = np.array([S0 - dS, S0, S0 + dS])[:, None]
    log_paths = np.zeros((3, N_PATHS, n_steps + 1))
    log_paths[:, :, 0] = np.log(starts)
    drift_vec = (r - q - 0.5 * vol ** 2) * dt
    sigma_vec = vol * np.sqrt(dt)
    for t in range(1, n_steps + 1):
        log_paths[:, :, t] = log_paths[:, :, t-1] + drift_vec + sigma_vec * Z[:, t-1]
    paths = np.exp(log_paths)
    pv = np.array([pv_one_path(paths[i, j]) for i in range(3) for j in range(N_PATHS)])
    pv = pv.reshape(3, N_PATHS).mean(axis=1)
    pv_pct = pv[1] / S0 * 100
    delta = (pv[2] - pv[0]) / (2 * dS)
    gamma = (pv[2] - 2 * pv[1] + pv[0]) / (dS ** 2)
    return pv_pct, delta, gamma

if __name__ == "__main__":
    t0 = time.time()
    pv, delta, gamma = price_and_greeks()
    print(f"PV(% notional) = {pv:.3f} %")
    print(f"Delta          = {delta:.4f}")
    print(f"Gamma          = {gamma:.6f}")
    print(f"Time used      = {time.time()-t0:.2f} s")
